# Security model

The same in plain terms, with how to revoke access and export your wallet: [copybara.trading/security](https://copybara.trading/security).

## Custody

**Copybara is noncustodial.**

- **Your wallet.** When you sign up you get your own trading wallet: one address for the EVM chains and one for Solana.
- **Your keys.** The keys are held by [Privy](https://privy.io), in secure hardware. Copybara never sees them.
- **Taking them with you.** You can export your keys from the website and use the wallet anywhere else.
- **Withdrawing.** You can send your funds back to your own wallet at any time.

## What Copybara is allowed to do

When you turn trading on, you allow Copybara to ask your wallet to sign some transactions, and only these:

- **Swaps** through approved exchanges and routers, for copies, your exit rules and your own sales.
- **Approvals of the exact amount** a swap needs, only to those approved exchanges. Never unlimited approvals to anyone else.
- **Moves between your own wallets,** such as bridging your funds to the chain a copy trades on.
- **Copybara's fee** on trades the bot makes. See [FEES.md](FEES.md).
- **Polymarket orders** on Polymarket's own exchange contracts, from your own Polymarket wallet, within your copy limits.

Anything else, such as sending your funds to someone else's address, is refused.

## How every transaction is checked

Every signing request goes through **two separate checks**:

1. **Privy's policy.** Rules held at Privy limit your wallet to approved contracts on approved chains.
2. **Copybara's guard.** A separate service checks every request before Privy signs it. For a trade, the guard:
   - **Simulates it** and refuses it unless what you buy lands in your own wallet and nothing else leaves it.
   - **Checks the price.** It fetches prices itself and refuses a swap that could fill far below what the tokens are worth.
   - **Checks the trigger.** It refuses a buy unless you are copying a wallet that just bought that same token. It reads that wallet's trade from the chain itself.
   - **Checks your settings.** It applies your copy's maximum per trade and your kill switch.
   - **Checks your approval.** Each copy you set up is approved by your own wallet. The guard checks that approval, so nobody else can create or change your copies, even with access to Copybara's servers.

For Polymarket bets, the guard checks the bet itself before signing:

- the exchange is Polymarket's;
- the bet is placed from your own wallet;
- the market is real and still open;
- the price is close to the live order book;
- the amount is within your limits;
- the bettor you copy really placed that bet.

## Stopping everything

- **Pause a copy** at any time from the Copy page.
- **The kill switch** stops all trading for your account at once. When you turn it on, you can also sell everything you hold.
- **Copybara can pause all trading,** or only new copies, across the platform in an emergency. Copies stop at once, and you can still withdraw.

## Your account

- **Sign-in.** You sign in with your email or your own wallet.
- **Sessions.** Each one is tied to your browser, and signing out ends it.
- **Your other wallets.** Linking your own wallet only proves you own it. Copybara never gets permission to move funds from it.

## Reporting a problem

See [SECURITY.md](../SECURITY.md).
