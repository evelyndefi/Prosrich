# Changelog

All notable changes to **Pharos Alpha** are documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Planned
- Block explorer deep-links (click block number → PharosScan)
- Gas price sparkline chart (last 10 readings)
- RPC latency display (ping time per endpoint)
- Light / dark theme toggle

---

## [1.1.0] — 2026-05-02

### Added
- Complete deep ocean blue redesign with lighthouse theme
- Animated SVG lighthouse with sweeping beam and pulsing lamp
- Rising bubble particle system (10 animated CSS bubbles)
- Star field in CSS background
- Ocean radial glow gradient backgrounds
- `Cinzel` serif display font for headings (replaced default system stack)
- `mainnet-badge` component: "Pacific Ocean Mainnet · LIVE"
- Community / social card section ("Join the Fleet") with 6 links:
  - X / Twitter (`@pharos_network`)
  - Discord (`discord.gg/pharos`)
  - Telegram (`@PharosNetworkOfficial`)
  - GitHub (`PharosNetwork`)
  - Ecosystem / Grants
  - Brand Kit
- Mini lighthouse icon in topbar brand mark
- `section-label` micro-labels above section headings
- `status` pill now has pulsing green dot animation
- Teal left-border accent on metric cards
- Gradient text treatment on `<h1>`
- `⚓ Pacific Ocean Mainnet` pill in topbar
- 3-column feature card row below hero
- Additional ecosystem links: `ecosystem`, `buildonpharos.com`, `brandkit`
- Terminal feed lines now include performance stats (TPS, block time)

### Changed
- Color palette: migrated from light `#f5f6f8` background to dark `#020810` abyss
- Accent: replaced lime green (`#d8ff63`) with deep teal (`#00b4d8`)
- All panel backgrounds are now dark glassmorphism with `backdrop-filter: blur`
- `hero-side` feature cards now use dark navy gradient instead of lime/dark split
- `link-grid` links now use teal-on-dark style instead of white pills
- Topbar now has `border-radius: 999px` pill shape retained but with dark treatment
- Hero copy color updated for dark background legibility
- Terminal feed is now near-black (`rgba(2,8,16,0.9)`) with teal text
- Section heads now use `Cinzel` serif font
- All shadows updated to use dark drop-shadow (removed light-mode `rgba` shadows)
- Signature footer now uses pill container with pulsing dot accents

### Fixed
- `loading` class text color updated for dark background visibility
- `metric-meta` color contrast improved for dark panel backgrounds
- Mobile grid collapse now properly handles all new sections

---

## [1.0.0] — 2026-04-28

### Added
- Initial release — live ecosystem surface for Pharos Network
- Dual-network RPC reads: mainnet (`rpc.pharos.xyz`) and testnet (`atlantic.dplabs-internal.com`)
- `eth_blockNumber`, `eth_gasPrice`, `net_version` — all three fetched in parallel per network
- Auto-refresh every 20 seconds via `setInterval`
- Terminal feed log with timestamped output
- `rpcCall()` — generic JSON-RPC 2.0 fetch wrapper with error handling
- `fetchNetwork()` — parallel Promise.all wrapper per endpoint
- `setLoaded()` — DOM update helper that removes `loading` CSS class on success
- Hero section with two-column layout (main + side cards)
- Feature cards: "Live Chain Pulse" and "Built for Builders"
- Network Pulse section: 4-up metric grid (mainnet block, testnet block, mainnet gas, testnet gas)
- Live Feed terminal panel
- Core Primitives section: x402, Circle CCTP, Oracles + SPNs
- Build Angles section: Agent Commerce, RealFi Infra, Builder Ops
- Useful References section with link grid
- "Why this works" panel: Live / No friction / Extensible
- Light theme with `#f5f6f8` background and `#d8ff63` lime green accent
- `Manrope` sans-serif + `JetBrains Mono` terminal font
- Responsive grid collapse at 1080px
- Topbar with brand mark, pills, and pill-shaped nav bar
- Signature footer: "Made with 🤍 for the Pharos Ecosystem · By Kennyy"

---

[Unreleased]: https://github.com/kennyy/pharos-alpha/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/kennyy/pharos-alpha/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/kennyy/pharos-alpha/releases/tag/v1.0.0
