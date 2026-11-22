# Architecture

Copybara has a website, an API and a few background services. Each does one job, and only one of them, the guard, can approve a signature.

```
 You ──► Website ──► API ──────────────► Database
                      │ (signs nothing)     ▲
                      ▼                     │
                   Job queue ◄──────► Worker ┤  watches chains, decides, builds trades
                                       │     │
                                       ▼     │
                              Guard (separate service) ──► Privy wallet signs ──► Chain
                                                                    │
                       Bets service (Polymarket) ───────────────────┘
```

## The parts

| Part | What it does | What it can't do |
|---|---|---|
| **Website** | Where you sign in, pick wallets or bettors to copy, set your rules and see your trades. | Hold keys or sign anything. |
| **API** | Your account, copies, settings, balances and history. It also takes in trade alerts from chain data providers. | Sign transactions. It never holds keys. |
| **Worker** | Watches the wallets being copied, decides whether to copy each trade, sizes it, builds the transaction and sends it once signed. It also runs your exit rules: take profit, stop loss, trailing stop and time limit. | Sign on its own, or create or change your copies. Its database login can't do that. |
| **Guard** | A separate service that checks every signing request against fixed rules before Privy signs it. See [SECURITY_MODEL.md](SECURITY_MODEL.md). | Be skipped: Privy only signs requests the guard has approved. |
| **Bets service** | Spots bets from the Polymarket bettors being copied, and places the copies on Polymarket. It runs in a region where Polymarket accepts orders. | Bet anywhere but Polymarket's own exchange contracts, or past your limits. |
| **Wallets (Privy)** | Holds your trading wallet's keys in secure hardware and signs only what the guard approves. | Be used by Copybara to see or export your keys. |

## How the parts talk

- **Jobs go through a queue.** Every job has an id taken from what triggered it, so the same trade arriving twice becomes one job.
- **The database is the record.** Unique keys make sure each trade is recorded once, each copy is made once, and each fee is booked once.
- **Signing goes one way.** The worker asks the guard, the guard checks and approves, and Privy signs. The worker never sees a key.
- **Each service has its own database login,** limited to what that service needs.

## Watching for trades

- **EVM chains** (Robinhood Chain, Elysium): live log subscriptions, with block-by-block polling as a backup.
- **Solana:** a live subscription to each copied wallet's activity, with webhooks as a backup.
- **Polymarket:** fills read from Polygon as each block lands, about every 2 seconds, with Polymarket's trade list as a backup.

All sources feed the same reader, which works out what the wallet actually bought or sold from its balance changes. It doesn't depend on which app or exchange the wallet used. That's why wallets trading through terminals such as FOMO, GMGN and Onagi can be copied too.

See [TRADING.md](TRADING.md) for what happens next.
