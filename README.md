# TREE Axelar Bridge Frontend

This is a static TREE bridge console for the Sui to BNB Chain Axelar route.

It does not custody funds or sign transactions. The final transfer step opens the official Axelar route:

```text
https://interchain.axelar.dev/sui/0x6c5a609f6d0288523ce4a6ed87d19ae127f62073ab75fd9b0b1c9b455d4895cf::tree::TREE
```

## What it does

- Shows the TREE on Sui to BNB Chain route.
- Validates a BNB destination wallet address.
- Lets users prepare and copy a transfer note.
- Saves recent transfer plans in local browser storage.
- Keeps a readiness checklist for small-test, destination, and gas checks.
- Gives BNB project lanes for liquidity, app payments, rewards, and holder access.
- Uses `assets/treetoken-logo.webp` for the header, favicon, route token label, and token identity panel.
- Uses `assets/tree-hero-city.jpg` as the top hero artwork.

## Configuration

Edit `config.js` when the route or destination details change:

```js
window.TREE_BRIDGE_CONFIG = {
  sourceTokenType: "...",
  officialAxelarRoute: "...",
  destinationTokenAddress: "",
  destinationLiquidityVenue: "",
};
```

`bridge-config.json` contains the same values in a plain data format for developer handoffs or deployment pipelines.

## Local use

Open `index.html` in a browser.

For a local server:

```powershell
python -m http.server 8899
```

Then open:

```text
http://localhost:8899/tree-axelar-bridge/
```

## Production notes

- Keep Axelar as the execution surface unless Axelar confirms an official embeddable widget or SDK flow for this route.
- Do not iframe `interchain.axelar.dev` unless Axelar explicitly supports it for this page.
- Once a BNB-side TREE token address and liquidity venue are confirmed, add those destination details to the route panel and project-lane cards.
- Keep the "test small first" copy visible for launch.
- The page does not connect wallets, ask for seed phrases, or custody funds.

## Design reference

The generated concept used for this pass is saved at:

```text
design/bridge-console-concept.png
```
