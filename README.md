# TREE Axelar Bridge Frontend

This repo contains a static TREE bridge frontend for the Sui to BNB Chain Axelar route.

It does not custody funds or sign transactions. The final transfer step opens the official Axelar route:

```text
https://interchain.axelar.dev/sui/0x6c5a609f6d0288523ce4a6ed87d19ae127f62073ab75fd9b0b1c9b455d4895cf::tree::TREE
```

## What it does

- Shows the TREE on Sui to BNB Chain route.
- Includes the TreeToken logo and hero artwork directly in `index.html` for a single-file static deploy.
- Validates a BNB destination wallet address.
- Lets users prepare and copy a transfer note.
- Keeps a readiness checklist for small-test, destination, and gas checks.
- Gives BNB project lanes for liquidity, app payments, rewards, and holder access.

## Configuration

The public page is self-contained in `index.html`.

`bridge-config.json` and `config.js` keep the same route values in developer-friendly formats for a fuller app pass or future build pipeline.

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

## Production notes

- Keep Axelar as the execution surface unless Axelar confirms an official embeddable widget or SDK flow for this route.
- Do not iframe `interchain.axelar.dev` unless Axelar explicitly supports it for this page.
- Once a BNB-side TREE token address and liquidity venue are confirmed, add those destination details to the route panel and project-lane cards.
- Keep the test-small-first copy visible for launch.
- The page does not connect wallets, ask for seed phrases, or custody funds.
