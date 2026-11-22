# Changelog

What changed in Copybara, newest first. Small fixes are grouped together.

## 22 November 2026

- **Status page:** [copybara.trading/status](https://copybara.trading/status) shows whether each part of Copybara is working, and any incidents.
- **Polymarket: real-money bet copying.** Bets are placed from the bets service and checked by the guard before signing. Paper copies stop once betting opens.
- **Polymarket: faster copies.** Bettors' bets are spotted on Polygon within seconds, not from Polymarket's trade list.
- **Polymarket: add money** from your Copybara wallet, and see how much arrives before you move it.
- **Polymarket: markets past their listed end time** are copied while they are still open.
- **Top bettors:** a new column shows how many bets each bettor placed in the last 24 hours, 48 hours, 72 hours, week or 2 weeks.
- **Home page:** a new FAQ.

## 21 November 2026

- **Polymarket: top bettors** are ranked by win rate, return and profit, and you can look up any bettor.
- **Polymarket: copy a bettor's bets**, with your own settings for each bettor:
  - bet size and price range;
  - time until the market ends, and market liquidity;
  - categories, and their minimum bet;
  - selling with them or holding to the result;
  - take profit, stop loss and spending limits.

## 20 November 2026

- **Fixes:**
  - stop losses skipped for low gas now run;
  - a backup for Elysium;
  - a more accurate sell quote.
- **Security update** to the website framework.

## 18 to 19 November 2026

- **Sale messages and PnL cards:** a "Sale succeeded" message, and a shareable profit-and-loss card for each position.
- **Sales work when ETH runs low,** and a warning says when it has run out.
- **Add ETH from your own wallet,** and trades skipped for lack of gas say so.
- **Roadmap page** redesign.

## 16 November 2026

- **Fees:** a flat 0.5% on every bot trade, with no extra fee on profitable sales.
- **Positions:** a live sell quote before you sell.
- **Wallet:**
  - see what each chain holds, coin by coin;
  - swap a chain's dollars and its own coin with no Copybara fee.
- **Activity:** filter by everything, bought, sold or skipped.
- **Copy settings:** a "Copy repeat buys" switch, with a maximum per token.
- **Faster EVM sends:** confirmations are checked at block speed.
- **Home page FAQ and Roadmap page.**

## 14 to 15 November 2026

- **Faster copies:** live log subscriptions on EVM chains.
- **Robinhood Chain:** trades route through an aggregator, including PONS launches.
- **Solana launchpad tokens** (pump.fun, Bags) can be copied before they graduate. A switch on the Copy page controls this.
- **Copies:**
  - price movement is checked on the live quote;
  - app accounts and addresses too busy to be one trader are refused.
- **Deposits:** USDC and USDG deposits bring $0.50 of the chain's own coin for network fees.
- **Activity:** pages of 10, 20 or 50 trades, and each trade opens to show its details, including your price next to the copied wallet's.
- **Wallet:** a Bridge button moves money between chains at any time.
- **Sign-in:** with a wallet or email only. Copies are approved silently by your own Copybara wallet, with no passkey prompts.
- **Website:** a stricter Content Security Policy.

## 12 to 13 November 2026

- **Private beta launch:** copy trading on Robinhood Chain, Solana and Elysium.
- **Paper trading** for test accounts.
- **Public backup nodes** keep copies running if the main data provider fails.
