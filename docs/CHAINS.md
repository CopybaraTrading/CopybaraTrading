# Supported chains

| Chain | Status | Deposit | Notes |
|---|---|---|---|
| **Robinhood Chain** | Live | ETH, USDG | Trades route through an aggregator, including tokens still on PONS's launchpad. |
| **Solana** | Live | SOL, USDC, USDT | Includes pump.fun and Bags launchpad tokens before they graduate, if you turn that on. |
| **Elysium** | Live | HYPE, USDC | Money moves in and out through HyperEVM. |
| **BNB Chain** | Coming soon | BNB, USDC | Built; switched off during the beta. |
| **Avalanche** | Coming soon | AVAX, USDC | Built; switched on after the other chains. |
| **Base** | Coming soon | ETH, USDC | Built; switched off during the beta. |
| **Ethereum** | Coming soon | ETH, USDC | Built; switched off during the beta. |
| **Polymarket** (Polygon) | Beta | USDC from several chains, converted to pUSD | Copies bets from Polymarket bettors. See below. |

## On every chain

- **One wallet per chain family.** Your EVM address is the same on every EVM chain. Solana has its own address.
- **Network fees.** Trades need a little of the chain's own coin (ETH, SOL, HYPE) for fees. A USDC or USDG deposit brings about $0.50 of it, and Copybara warns you when it runs low.
- **Moving money between chains.** The Wallet page's Bridge button moves funds between your own wallets. A copy can also bring funds to its chain when you set it up.
- **Any wallet can be copied,** including wallets trading through terminals. Exchange and app accounts shared by many people, and addresses far busier than one trader, are refused, because they aren't one person's trades.

## Limits

- **Speed depends on the chain.** A copy follows within seconds, but no copy can land in the same block as the trade it copies.
- **Thin markets.** In tokens with little liquidity, a copy can get a different price from the wallet it copies. The price-movement check skips a trade when the gap is too large.
- **Odd transactions.** Transactions too tangled to read safely aren't copied.

## Polymarket

- **Where it works.** Polymarket doesn't accept new bets from some countries. Copybara checks your location before copying bets for you. Where only closing is allowed, your open bets can still be sold.
- **Your Polymarket wallet.** Bets are placed from your own Polymarket wallet, which your Copybara wallet controls. Polymarket's relayer pays the Polygon network fees.
- **Adding money.** Add money from your Copybara wallet, or deposit USDC from another chain.
- **Coming soon:**
  - collecting winnings from bets held to the result;
  - moving money out of your Polymarket balance from the website.
