<div align="center">

<!-- LIGHTHOUSE ASCII ART -->
```
         *
        /|\
       / | \
      /  |  \
     /   |   \
    /    |    \
   /_____|_____\
        |||
        |||
        |||
   ~~~~~|||~~~~~
  ~~~~~~~~~~~~~
```

# ⚓ Pharos Alpha

**A live, builder-facing ecosystem surface for the [Pharos Network](https://pharos.xyz)**

[![License: MIT](https://img.shields.io/badge/License-MIT-00b4d8.svg?style=for-the-badge)](./LICENSE)
[![Network: Mainnet](https://img.shields.io/badge/Network-Pacific%20Ocean%20Mainnet-0d2148?style=for-the-badge&logo=ethereum)](https://pharos.xyz)
[![Chain: EVM](https://img.shields.io/badge/Chain-EVM%20Compatible-1459a0?style=for-the-badge)](https://docs.pharos.xyz)
[![Status: Live](https://img.shields.io/badge/Status-Live-00b4d8?style=for-the-badge&logo=statuspage)](https://rpc.pharos.xyz)
[![Made by: Kennyy](https://img.shields.io/badge/Made%20by-Kennyy-090f24?style=for-the-badge)](https://github.com/kennyy)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-48cae4?style=for-the-badge)](./CONTRIBUTING.md)

<br/>

> *A single-file, zero-dependency ecosystem dashboard that reads live data directly from Pharos public RPC endpoints — no wallet required, no backend needed.*

<br/>

[**Live Demo**](https://pharos.xyz) · [**Report a Bug**](.github/ISSUE_TEMPLATE/bug_report.md) · [**Request a Feature**](.github/ISSUE_TEMPLATE/feature_request.md) · [**Read the Docs**](./docs/ARCHITECTURE.md)

</div>

---

## 📖 Table of Contents

- [About the Project](#-about-the-project)
- [Features](#-features)
- [Architecture](#-architecture)
- [Quick Start](#-quick-start)
- [Configuration](#️-configuration)
- [Network Reference](#-network-reference)
- [Ecosystem Links](#-ecosystem-links)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [License](#-license)
- [Acknowledgments](#-acknowledgments)

---

## 🌊 About the Project

**Pharos Alpha** is a clean, production-grade ecosystem dashboard for [Pharos Network](https://pharos.xyz) — the fastest EVM-compatible Layer 1 blockchain, built by ex-Ant Financial engineers for Real-World Asset (RWA) tokenization and institutional-grade DeFi.

This project was built as a **community contribution** to give developers, researchers, and builders a fast, transparent entry point into the Pharos ecosystem. It reads live chain data directly from public RPC endpoints, with zero wallet prompts, zero backend, and zero bloat.

### Why this exists

Most blockchain ecosystem pages are either marketing sites or full dApps requiring wallet connections. Pharos Alpha sits in between: a **live technical surface** that shows real chain data and links to everything a builder actually needs.

### Pharos Network — at a glance

| Property | Value |
|---|---|
| Architecture | Modular Full-Stack Parallel L1 |
| Consensus | AsyncBFT |
| VM Support | EVM + WASM (dual) |
| TPS | 50,000+ |
| Block Time | ~0.2 seconds |
| Finality | Sub-second |
| Native Token | PROS |
| Focus | RWAfi, DeFi, AI, Payments |
| Mainnet | Pacific Ocean Mainnet (April 2026) |
| Series A | $44M — Sumitomo, Chainlink, Flow Traders |

---

## ✨ Features

### Core

- **🔴 Live RPC Reads** — pulls block height, gas price, and chain ID from both mainnet and Atlantic testnet every 20 seconds
- **📡 Dual Network Coverage** — simultaneous reads from mainnet (`rpc.pharos.xyz`) and testnet (`atlantic.dplabs-internal.com`)
- **💻 Terminal Feed** — a live operational log styled as a developer terminal
- **⚡ Zero Dependencies** — single HTML file, no npm, no bundler, no backend
- **🌊 No Wallet Required** — fully public-facing, no MetaMask prompt, no permission step

### Design

- **🏯 Lighthouse Theme** — animated SVG lighthouse with sweeping beam, ocean waves, and rising bubble particles
- **🌌 Deep Ocean Palette** — dark maritime aesthetic with teal accents, foam highlights, and a star field background
- **📱 Responsive Layout** — collapses gracefully to a single-column layout on mobile
- **🎨 CSS-Only Animations** — bubbles, beam sweep, light pulse, and glow effects — all pure CSS, no JS animation library

### Ecosystem Surface

- **🔗 All Official Links** — main site, docs, devhub, testnet, explorers, grant program, brand kit
- **💬 Community Channels** — X/Twitter, Discord, Telegram, GitHub
- **🏗️ Primitive Coverage** — x402, Circle CCTP, Oracles, SPNs, Chainlink CCIP
- **📋 Build Angles** — agent commerce, RealFi infra, builder ops layer

---

## 🏗️ Architecture

Pharos Alpha is intentionally a **single-file static site**. Here is how it is structured internally:

```
pharos_alpha.html
│
├── <style>                     CSS Variables + Full Stylesheet
│   ├── :root {}                Design tokens (colors, radii, shadows)
│   ├── body::before / ::after  Ocean background + star field
│   ├── .bubbles / .bubble      Animated rising bubble particles
│   ├── .page / .panel          Layout grid + glassmorphism panels
│   ├── .lighthouse-svg         Animated lighthouse (beam + light pulse)
│   ├── .hero / .hero-side      Two-column hero layout
│   ├── .metrics                 4-up stat grid
│   ├── .feed                   Monospaced terminal feed
│   ├── .social-section         6-up community card grid
│   └── @media (max-width)      Responsive breakpoints
│
├── <body>                      DOM Structure
│   ├── .bubbles                10 animated bubble elements
│   ├── .topbar                 Nav bar with mini lighthouse icon
│   ├── .hero                   Main heading + animated lighthouse SVG
│   ├── Feature cards (3-up)    Chain pulse / Performance / Builders
│   ├── Network Pulse + Feed    Live metrics + terminal
│   ├── Core Primitives         x402 / CCTP / Oracles
│   ├── Build Angles            Agent commerce / RealFi / Ops
│   ├── References              Endpoints + Explorer links
│   ├── Why this works          Trust + extensibility
│   ├── Join the Fleet          6 social/community cards
│   └── .signature              Kennyy attribution footer
│
└── <script>                    RPC Logic
    ├── rpcCall()               JSON-RPC 2.0 fetch wrapper
    ├── fetchNetwork()          Parallel eth_blockNumber + eth_gasPrice + net_version
    ├── refresh()               Full dual-network update cycle
    └── setInterval(refresh, 20000)   Auto-refresh every 20 seconds
```

### Data Flow

```
Browser                     Pharos RPC
   │                            │
   ├─ fetch POST ──────────────►│  eth_blockNumber
   ├─ fetch POST ──────────────►│  eth_gasPrice
   ├─ fetch POST ──────────────►│  net_version
   │                            │
   │◄── JSON response ──────────┤
   │                            │
   ├─ hexToInt(block)           │
   ├─ weiToGwei(gas)            │
   ├─ update DOM elements       │
   └─ log to terminal feed      │
```

No intermediate server. No API key. No wallet. Just the browser talking directly to the public RPC.

---

## 🚀 Quick Start

### Option 1 — Open directly (recommended)

```bash
# Clone the repo
git clone https://github.com/kennyy/pharos-alpha.git
cd pharos-alpha

# Open in your browser — that's it
open src/pharos_alpha.html        # macOS
xdg-open src/pharos_alpha.html    # Linux
start src/pharos_alpha.html       # Windows
```

### Option 2 — Serve locally (for development)

```bash
# Using Python (no install required)
python3 -m http.server 8080
# then visit http://localhost:8080/src/

# Using Node.js (npx, no install required)
npx serve .
# then visit the URL shown in your terminal

# Using VS Code
# Install the Live Server extension and click "Go Live"
```

### Option 3 — Deploy to static hosting

The project is a single HTML file — it deploys anywhere:

| Platform | Command |
|---|---|
| **Vercel** | `vercel --prod` |
| **Netlify** | Drag-and-drop `src/` folder |
| **GitHub Pages** | Push to `gh-pages` branch |
| **Cloudflare Pages** | Connect repo, build command: `echo done` |
| **IPFS** | `ipfs add src/pharos_alpha.html` |

---

## ⚙️ Configuration

All configuration lives inside the `<script>` block in `src/pharos_alpha.html`.

### RPC Endpoints

```javascript
const endpoints = {
  mainnet: 'https://rpc.pharos.xyz',
  testnet: 'https://atlantic.dplabs-internal.com'
};
```

To point at a different RPC (e.g. a local node or private endpoint), just update these values.

### Refresh Interval

```javascript
setInterval(refresh, 20000);  // 20,000ms = 20 seconds
```

Change `20000` to any value in milliseconds. Be mindful of rate limits on public RPC endpoints.

### Adding a New RPC Method

The `rpcCall()` function is a generic JSON-RPC 2.0 wrapper. Calling any new method is one line:

```javascript
// Example: fetch latest block object
const block = await rpcCall(endpoints.mainnet, 'eth_getBlockByNumber', ['latest', false]);
```

---

## 🌐 Network Reference

### Mainnet — Pacific Ocean Mainnet

| Property | Value |
|---|---|
| RPC | `https://rpc.pharos.xyz` |
| Explorer | [pharosscan.xyz](https://www.pharosscan.xyz) |
| SocialScan | [pharos.socialscan.io](https://pharos.socialscan.io) |
| CCTP Domain | 31 |

### Testnet — Atlantic

| Property | Value |
|---|---|
| RPC | `https://atlantic.dplabs-internal.com` |
| Explorer | [atlantic.pharosscan.xyz](https://atlantic.pharosscan.xyz) |
| Faucet | [testnet.pharosnetwork.xyz](https://testnet.pharosnetwork.xyz) |

### Supported RPC Methods

| Method | Description |
|---|---|
| `eth_blockNumber` | Latest block height |
| `eth_gasPrice` | Current gas price (hex wei) |
| `net_version` | Chain ID |
| `eth_getBlockByNumber` | Block object (not used in v1, extensible) |
| `eth_call` | Contract reads (extensible) |

---

## 🔗 Ecosystem Links

### Official

| Resource | URL |
|---|---|
| Main Site | [pharos.xyz](https://pharos.xyz) |
| Docs | [docs.pharos.xyz](https://docs.pharos.xyz) |
| DevHub | [pharos.xyz/devhub](https://pharos.xyz/devhub) |
| Testnet | [testnet.pharosnetwork.xyz](https://testnet.pharosnetwork.xyz) |
| Ecosystem | [pharos.xyz/ecosystem](https://pharos.xyz/ecosystem) |
| Grants ($10M) | [pharos.xyz/ecosystem](https://pharos.xyz/ecosystem) |
| Builder Base Camp | [buildonpharos.com](https://www.buildonpharos.com) |
| Brand Kit | [pharos.xyz/brandkit](https://pharos.xyz/brandkit) |

### Explorers

| Explorer | URL |
|---|---|
| PharosScan (Mainnet) | [pharosscan.xyz](https://www.pharosscan.xyz) |
| PharosScan (Testnet) | [atlantic.pharosscan.xyz](https://atlantic.pharosscan.xyz) |
| SocialScan | [pharos.socialscan.io](https://pharos.socialscan.io) |

### Community

| Channel | Link |
|---|---|
| X / Twitter | [@pharos_network](https://x.com/pharos_network) |
| Discord | [discord.gg/pharos](https://discord.gg/pharos) |
| Telegram | [@PharosNetworkOfficial](https://t.me/PharosNetworkOfficial) |
| GitHub | [github.com/PharosNetwork](https://github.com/PharosNetwork) |

---

## 🗺️ Roadmap

### v1.0 — Current

- [x] Live dual-network RPC reads (mainnet + testnet)
- [x] Auto-refresh every 20 seconds
- [x] Terminal feed with live log output
- [x] Deep ocean lighthouse theme
- [x] Animated SVG lighthouse with beam sweep
- [x] Rising bubble particle system
- [x] Full ecosystem link surface
- [x] Community / social card grid
- [x] Responsive mobile layout

### v1.1 — Next

- [ ] Block explorer deep-links (click block number → PharosScan)
- [ ] Transaction count ticker (via explorer API)
- [ ] Gas price sparkline chart (last 10 readings)
- [ ] Light / dark theme toggle
- [ ] RPC latency display (ping time per endpoint)

### v2.0 — Planned

- [ ] Multi-RPC fallback with health scoring
- [ ] SPN (Special Processing Network) status panel
- [ ] CCTP cross-chain transfer tracker
- [ ] x402 micropayment reference UI
- [ ] On-chain activity heatmap
- [ ] ENS / Pharos name resolution

### Community Ideas

Have an idea? [Open a feature request](https://github.com/kennyy/pharos-alpha/issues/new?template=feature_request.md) — all suggestions welcome.

---

## 🤝 Contributing

Contributions make the open-source community what it is. Any contribution you make is **genuinely appreciated**.

Read our full contribution guide: [**CONTRIBUTING.md**](./CONTRIBUTING.md)

**Quick contribution steps:**

```bash
# 1. Fork the repo (click Fork on GitHub)

# 2. Clone your fork
git clone https://github.com/YOUR_USERNAME/pharos-alpha.git

# 3. Create a feature branch
git checkout -b feature/your-feature-name

# 4. Make your changes
# (edit src/pharos_alpha.html)

# 5. Commit with a descriptive message
git commit -m "feat: add gas price sparkline chart"

# 6. Push to your fork
git push origin feature/your-feature-name

# 7. Open a Pull Request on GitHub
```

See [CONTRIBUTING.md](./CONTRIBUTING.md) for detailed guidelines, commit conventions, and code style.

---

## 📄 License

Distributed under the **MIT License**. See [LICENSE](./LICENSE) for full text.

```
MIT License — you are free to use, modify, and distribute this project
with attribution. See LICENSE for details.
```

---

## 🙏 Acknowledgments

- [**Pharos Network**](https://pharos.xyz) — for building the chain worth building on
- [**@pharos_network**](https://x.com/pharos_network) — the community of 500K+ sailors
- [**JetBrains Mono**](https://www.jetbrains.com/legalnotices/terms-of-use-jetbrains-mono/) — terminal font
- [**Cinzel**](https://fonts.google.com/specimen/Cinzel) — display typeface
- [**Google Fonts**](https://fonts.google.com) — open font hosting
- Every builder exploring Pharos before the tide gets crowded 🌊

---

<div align="center">

Made with 🌊 for the Pharos Ecosystem

**By Kennyy** · [@kennyy](https://github.com/kennyy)

⚓ *The lighthouse is lit. Set sail.*

</div>
