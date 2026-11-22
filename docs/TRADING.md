# Trade execution

How a trade by a wallet you copy becomes your trade.

## 1. Spotting the trade

Copybara watches every wallet being copied, live, on each chain (see [ARCHITECTURE.md](ARCHITECTURE.md)). The same trade can arrive from more than one source, but it is recorded once.

Copybara reads the whole transaction and works out what the wallet actually bought or sold from its balance changes. Transfers, airdrops and swaps between two stablecoins aren't trades, so they aren't copied. Neither are transactions too tangled to read safely.

## 2. Deciding whether to copy it

Each check runs in order. If one fails, the trade is skipped and the reason shows in your **Activity** page.

1. **Trading is on.** Neither the platform pause nor your kill switch is on, and the copy isn't paused.
2. **The trade is big enough.** It's skipped if it's smaller than your "their minimum trade".
3. **Not too many trades.** It's skipped if the wallet trades faster than your trades-per-hour limit.
4. **Your loss limits.** A copy that hits them pauses itself.
5. **Token safety.** Known scam tokens, honeypots and tokens with too little liquidity are skipped. You choose whether to copy launchpad tokens that haven't graduated yet.
6. **Price movement.** It's skipped if the price has already moved too far past the price they got.
7. **Your balance.** It's skipped if you don't have enough to make the trade and pay network fees.
8. **Size.** Your copy's size comes from your setting: a fixed dollar amount, a share of your balance, a multiple of their trade, or the same share of your portfolio as theirs. It is kept within your per-trade and per-token maximums.

## 3. Making the trade

1. **Quote.** Copybara gets a quote from approved exchanges, with your slippage limit.
2. **Check and sign.** The guard checks the trade and simulates it, and only then does Privy sign it (see [SECURITY_MODEL.md](SECURITY_MODEL.md)).
3. **Send once.** The signed transaction is saved before it is sent. If anything restarts mid-way, the same transaction is resent, never a second one.
4. **Confirm.** Copybara waits for the chain to confirm it, then reads the real result back from the chain. Your position and Activity show what you actually got, not the quote.

## 4. When something fails

| What happened | What Copybara does |
|---|---|
| **A buy fails**, for example because the price moved past your slippage | It isn't retried: the moment has passed. Activity shows why. |
| **A sale fails** | It is retried up to 5 times, allowing more price movement each time, up to 30%. |
| **A transaction gets stuck** (EVM) | The same transaction is resent, or replaced with a higher fee using the same slot, so only one can ever go through. |
| **A transaction expires** (Solana) | It is resent until it expires. Only then is the chain's history checked, and a new one is built only if the first never landed. |
| **The chain reorganises** and drops a trade | Copybara waits for confirmations, re-checks that the block is still on the chain, and resends if it isn't. |
| **A copied trade disappears** in a reorganisation | The copy is flagged in Activity. A trade already made can't be undone. |
| **A service restarts** mid-trade | Trades left unfinished are picked up again from where they stopped. |

Copybara's fee is only taken on trades that go through.

## 5. Selling

For each copy, you choose how to exit:

- **Sell when they sell.** When they sell part of a token, you sell the same share of yours.
- **Your own exits.** Take-profit levels, a stop loss, a trailing stop and a time limit, checked every few seconds.
- **Both.** Whichever comes first.

If you sell with them, a stop loss still stays on as a safety net. You can also sell any position yourself from the **Positions** page.

## Polymarket bets

Copying a bettor works the same way, with a few differences:

- **Spotting.** Their bets are read from Polygon as each block lands, about every 2 seconds.
- **Checks.** Your copy settings are checked first: the price range, price movement, time until the market ends, market liquidity, categories, their minimum bet, and your daily, per-market and open-bet limits.
- **Placing.** The bet is placed as a fill-or-kill order with a price limit. It fills at once at your price or better, or not at all.
- **Selling.** When they sell, you sell the same share, unless you chose to hold to the result. Your own take profit and stop loss can also sell.
