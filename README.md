# Phantom Demo — Build 136

A local wallet UI simulation. Balances, trades, funding and chat messages are demo data. Market prices and available historical charts come from external data providers.

## Open the app

- Open `www/phantom-standalone.html` for the single-file version.
- Serve `www/` with a local web server for the installable web app. For example, run `python -m http.server 8080 --directory www`, then open http://localhost:8080.
- The existing `.github/workflows/main.yml` packages the prebuilt `www/` assets into an unsigned iOS app. Signing and sideloading remain separate.

## Build 136 Home cards

Token and stock holdings use flat dark-grey rounded cards with 7px gaps, 70px minimum height, 36px logos and compact typography. The Cash card uses the same grey and corner shape. These styles apply to newly purchased holdings too.

## Included changes

- Swipe up over the Home balance to refresh prices, with a spinning gear. The existing pull-down gesture is preserved.
- Cash uses a banknote icon. Home token logos are bundled to match the supplied visual reference.
- Token detail → Trade opens Buy, Sell and Swap actions. Buying and selling include a payment/receive asset picker, separate amount-unit control, Review, Confirm, processing, completion and failure screens.
- Swap and Add Cash also go through Review. Confirmation checks balances, quote expiry and repeat submission before updating local holdings.
- Review uses the reference's black layout, large amount, Buy/Payment/Frequency rows and lavender confirmation button. Detail and settings drawers use rounded bottom sheets.
- Historical charts use returned timestamps, price/time inspection for line charts and OHLC inspection for candles. Unsupported or unavailable history shows an empty state with retry. LIVE requests refresh every minute using the available daily OHLC endpoint; it is not a tick-by-tick feed.
- Asset pages have a Live Chat preview. Avatar → Chats opens searchable token and market rooms. Rooms include local messages, long-press reactions, message deletion and a Trade shortcut. Prediction sheets include a chat entry point.
- Modal entry/dismissal, chart changes, message arrival and trade status have transitions, with reduced-motion support.

## Demo limits and visual fidelity

No blockchain transaction, payment-provider checkout or remote chat service is connected. The fee displayed in Review is a fixed demo assumption, not a live provider quote. Frequency stays at one-time purchase; recurring execution is not implemented. Slippage controls preview preferences and do not change the fixed demo quote. Perps chat links to the app's existing Perps list.

Official screenshots informed the Review layout and chart controls. Complete current chat screens and exact animation timings were not available in the references, so those details are approximations. The requested spinning gear is a customization.

See `INTERACTION_REFERENCES.md` for the research sources and `ICON_SOURCES.md` for icon sources.

## Rebuild after source edits

Requires Node.js and npm:

```sh
npm install
npm run build
```

The build writes `www/app.js`, `www/styles.css`, and `www/phantom-standalone.html`. Commit those files before running the existing IPA workflow. The build preserves the original bundled React runtime in `build/vendor-runtime.prefix.js`; the editable app is in `App.jsx`, `InteractionUI.jsx`, `trade-model.js`, and `interaction.css`.

## Build status

The web bundle and standalone HTML were rebuilt with esbuild. Runtime and device tests were not run for this update.

Earlier notes supplied with the project are retained in `build/LEGACY_BUILD_NOTES.md`.
