# Nephrite Mobile UI

A lightweight, mobile-optimized DApp UI for the Nephrite confidential stablecoin protocol on the [Beam](https://beam.mw) blockchain.

Nephrite is a collateralized stablecoin system (similar to Liquity) where users can open Troves, deposit collateral (BEAM), and borrow NPH stablecoins pegged to $1 USD.

## Features

**Dashboard**
- Nephrite ecosystem stats: TVL, active troves, NPH supply, stability pool size, TCR, issuance fee, recovery mode status, recovery mode price threshold
- My position: ICR, total NPH debt, stability pool deposit
- Quick-access action cards

**Trove Management**
- Open Trove with auto-calculated collateral (120% ICR target)
- Adjust Trove: withdraw/deposit collateral, borrow/repay NPH (separate screens)
- Advanced mode for simultaneous collateral + debt changes
- Real-time prediction: ICR, liquidation reserve, issuance fee, total debt
- Surplus collateral claim

**Stability Pool**
- Deposit/withdraw NPH to earn BEAM and BEAMX rewards
- Pool share percentage display
- Estimated pool share after deposit/withdrawal
- Earned rewards display
- Surplus claim

**Liquidation**
- View all troves sorted by collateral ratio
- "My trove" badge highlighting
- Initiate batch liquidation (up to 10 troves)
- 10 NPH reward per liquidated trove

**Redemption**
- Redeem NPH for BEAM at face value
- Real-time fee preview
- Net BEAM received display

## Technical Details

- **Single-file vanilla JS** — no frameworks, no build step (~39KB packaged)
- **Same contract** as the official Nephrite DApp (CID: `b8944fd3f6a62697a89b2a55acd1cb2e3893dadece99569706efa1da847dd440`)
- **Same app shader** (`nephriteAppShader.wasm`)
- Compatible with Beam Desktop Wallet (Qt WebChannel) and Android WebView (PriviMW Wallet)
- Event-driven refresh via `ev_subunsub` (no polling)
- Two-step transaction flow: `invoke_contract` → `process_invoke_data`

## Project Structure

```
nephrite-mobile-ui/
├── ui/
│   └── index.html              # Source (single-file DApp)
├── build/
│   ├── manifest.json           # DApp manifest
│   └── app/
│       ├── index.html          # Build copy
│       ├── nephriteAppShader.wasm
│       ├── appicon.svg         # DApp store icon
│       ├── nph-coin.svg        # NPH token icon
│       └── beam.svg            # BEAM token icon
└── releases/
    └── NephriteMobile.dapp     # Packaged DApp (ZIP)
```

## Building

The DApp is a single HTML file with inline CSS and JS. No build step required.

To package the `.dapp` file:

```bash
cd build
7z a -tzip ../releases/NephriteMobile.dapp manifest.json app/
```

## Installation

### From .dapp file
Install `releases/NephriteMobile.dapp` in the Beam Desktop Wallet or PriviMW Wallet via the DApp manager.

## Nephrite Protocol

- **Troves**: Collateralized debt positions — deposit BEAM, borrow NPH
- **Stability Pool**: Deposit NPH to earn BEAM/BEAMX from liquidations
- **Liquidation**: Undercollateralized troves (ICR < 110%) can be liquidated
- **Redemption**: Exchange NPH for BEAM at face value (0.5%+ fee)
- **Recovery Mode**: Activates when system TCR < 150%

## Documentation

- [Nephrite Manifesto](https://drive.proton.me/urls/SK5DXN4DNG#ALVvWMTkfayD)
- [Security Audit by Pessimistic](https://www.scribd.com/document/641181034/Beam-StableCoin-Security-Analysis-by-Pessimistic?secret_password=djjynkOuDy0wRZh6rErI)

## License

MIT
