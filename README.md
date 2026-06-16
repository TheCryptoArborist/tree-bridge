# TREE Direct Bridge Frontend

This repo contains a TREE bridge frontend for a direct Sui to BNB Chain flow.

The page is now direct-mode first: users connect a Sui wallet, enter a BNB destination wallet, and prepare a bridge intent without being sent straight to the Axelar bridge site. Final signing is intentionally launch-locked until the Axelar Sui route constants are verified and added.

Temporary fallback route:

```text
https://interchain.axelar.dev/sui/0x6c5a609f6d0288523ce4a6ed87d19ae127f62073ab75fd9b0b1c9b455d4895cf::tree::TREE
```

## What it does

- Shows the TREE on Sui to BNB Chain route.
- Detects/connects Sui wallets where Wallet Standard or injected wallet APIs are available.
- Validates a BNB destination wallet address.
- Lets users prepare and copy a direct bridge intent.
- Saves recent bridge intents in local browser storage.
- Keeps a readiness checklist for small-test, destination, and gas checks.
- Shows the launch lock and the exact constants needed before real signing is enabled.
- Gives BNB project lanes for liquidity, app payments, rewards, and holder access.

## Configuration

`config.js` and `bridge-config.json` carry the direct bridge scaffold:

```js
window.TREE_BRIDGE_CONFIG = {
  executionMode: "direct-sui-wallet",
  directBridge: {
    enabled: false,
    tokenId: "",
    itsPackageId: "",
    itsObjectId: "",
    gatewayPackageId: "",
    gatewayObjectId: "",
    gasServicePackageId: "",
    gasServiceObjectId: "",
    destinationChainAxelarKey: "",
  },
};
```

## Direct bridge launch checklist

Keep `directBridge.enabled` set to `false` until all of the following are verified against official Axelar/Sui sources and tested with a tiny transfer:

- Axelar ITS token ID for TREE.
- Axelar Sui ITS package and shared object IDs.
- Axelar Sui gateway package and shared object IDs.
- Axelar Sui gas service package and shared object IDs.
- Axelar destination-chain key for BNB Chain.
- TREE decimals and smallest-unit amount handling.
- Final Sui transaction builder for the Axelar ITS calls.

## Local use

Open `index.html` in a browser.

For a local server:

```powershell
python -m http.server 8899
```

Then open:

```text
http://localhost:8899/
```

## Netlify

This repo is ready for a static Netlify deploy. The `netlify.toml` file publishes the repo root.

The fuller local deployment folder at `C:\Users\peter\OneDrive\Documents\Thickquidity\tree-bridge-netlify-deploy` includes the separate CSS, JavaScript, and image assets. The GitHub `index.html` is kept as a compact self-contained fallback page for connector-based updates.

## Production notes

- Use the in-page Sui wallet flow as the primary user experience.
- Keep the Axelar route as a fallback until direct signing is fully verified.
- Do not iframe `interchain.axelar.dev` unless Axelar explicitly supports it for this page.
- Once a BNB-side TREE token address and liquidity venue are confirmed, add those destination details to the route panel and project-lane cards.
- Keep the test-small-first copy visible for launch.
- The page should never ask for seed phrases or custody funds.
