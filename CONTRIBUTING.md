# Contributing to Pharos Alpha

First off — thank you for taking the time to contribute. 🌊

Every pull request, bug report, and suggestion helps make this a better resource for the entire Pharos builder community. This document outlines the standards and process for contributing to this project.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [I Have a Question](#i-have-a-question)
- [How to Contribute](#how-to-contribute)
  - [Reporting Bugs](#reporting-bugs)
  - [Suggesting Features](#suggesting-features)
  - [Your First Pull Request](#your-first-pull-request)
  - [Improving Documentation](#improving-documentation)
- [Development Setup](#development-setup)
- [Code Style Guide](#code-style-guide)
- [Commit Message Convention](#commit-message-convention)
- [Pull Request Process](#pull-request-process)
- [Design Principles](#design-principles)

---

## Code of Conduct

This project follows our [Code of Conduct](./CODE_OF_CONDUCT.md). By participating, you agree to uphold it. Please report unacceptable behavior to the maintainers.

---

## I Have a Question

> **Before opening an issue**, please search [existing issues](https://github.com/kennyy/pharos-alpha/issues) — your question may already be answered.

For quick questions about the Pharos Network itself, the best place is:
- [Pharos Discord](https://discord.gg/pharos)
- [Pharos Docs](https://docs.pharos.xyz)
- [Pharos X / Twitter](https://x.com/pharos_network)

For questions about this project specifically, open a [GitHub Discussion](https://github.com/kennyy/pharos-alpha/discussions) or a [Q&A issue](https://github.com/kennyy/pharos-alpha/issues/new?template=question.md).

---

## How to Contribute

### Reporting Bugs

A good bug report is specific and reproducible. Before submitting:

1. Check the [existing issues](https://github.com/kennyy/pharos-alpha/issues) to avoid duplicates
2. Test on the latest version of the `main` branch
3. Confirm whether the issue is with the project code or with the Pharos RPC endpoints themselves (endpoints can degrade independently)

**Use the [bug report template](.github/ISSUE_TEMPLATE/bug_report.md) and include:**

- Your browser + version
- Steps to reproduce (be specific — what you clicked, what URL you were on)
- What you expected to happen
- What actually happened
- Screenshots or console logs if relevant
- Whether the RPC endpoints themselves were reachable at the time

> **Security vulnerabilities** — do **not** open a public issue. Email the maintainer directly. See [SECURITY.md](./SECURITY.md).

---

### Suggesting Features

Feature requests are welcomed. Use the [feature request template](.github/ISSUE_TEMPLATE/feature_request.md).

Good feature requests:
- Explain the **problem** you are solving, not just the implementation
- Stay within the project's scope (builder-facing, no-wallet, public-data surface)
- Reference the [roadmap in README.md](./README.md#roadmap) — check if it is already planned

The project has a deliberate scope: **live public data, no wallet, no backend.** Features that require authentication, private keys, or a server are outside scope (but feel free to fork and extend!).

---

### Your First Pull Request

Not sure where to start? Look for issues labeled:

| Label | Meaning |
|---|---|
| `good first issue` | Low complexity, great for new contributors |
| `help wanted` | Maintainer is specifically asking for help |
| `bug` | Confirmed bug needing a fix |
| `enhancement` | Agreed-upon feature ready for implementation |
| `docs` | Documentation improvements |

**Steps:**

```bash
# 1. Fork the repository on GitHub

# 2. Clone your fork locally
git clone https://github.com/YOUR_USERNAME/pharos-alpha.git
cd pharos-alpha

# 3. Add the upstream remote (to keep in sync)
git remote add upstream https://github.com/kennyy/pharos-alpha.git

# 4. Create a branch (see naming convention below)
git checkout -b feat/gas-sparkline

# 5. Make your changes in src/pharos_alpha.html

# 6. Test locally — open the file in your browser
open src/pharos_alpha.html

# 7. Commit your changes (see commit conventions below)
git add .
git commit -m "feat: add gas price sparkline for last 10 readings"

# 8. Push to your fork
git push origin feat/gas-sparkline

# 9. Open a Pull Request from your fork to the main repo
```

**Branch naming:**

| Type | Format | Example |
|---|---|---|
| Feature | `feat/short-description` | `feat/block-explorer-links` |
| Bug fix | `fix/short-description` | `fix/testnet-rpc-timeout` |
| Documentation | `docs/short-description` | `docs/update-network-table` |
| Style / design | `style/short-description` | `style/mobile-metric-cards` |
| Refactor | `refactor/short-description` | `refactor/rpc-error-handling` |

---

### Improving Documentation

Documentation contributions are just as valuable as code. Things you can improve:

- Fix typos or unclear language in `README.md`
- Expand the architecture section in `docs/ARCHITECTURE.md`
- Add examples to `docs/CUSTOMIZATION.md`
- Improve inline comments in the `<script>` block
- Add or improve JSDoc-style comments on functions

For documentation-only changes, you do **not** need to run any build process — just edit and submit a PR.

---

## Development Setup

This project has **zero build tooling**. Development is as simple as:

```bash
# Clone and open
git clone https://github.com/kennyy/pharos-alpha.git
open pharos-alpha/src/pharos_alpha.html
```

For a slightly better DX with auto-reload on save:

```bash
# Option A: Python simple server
cd pharos-alpha
python3 -m http.server 3000
# Open: http://localhost:3000/src/pharos_alpha.html

# Option B: Node serve (npx, no install)
npx serve pharos-alpha
# Open the URL it shows you

# Option C: VS Code Live Server extension
# Install "Live Server" by Ritwick Dey, then right-click pharos_alpha.html → Open with Live Server
```

**Browser DevTools** — the browser console will show any RPC errors. The `refresh()` function logs network failures explicitly.

---

## Code Style Guide

Since this is a single-file HTML project, the style conventions apply across CSS, HTML, and JavaScript.

### General

- Indent with **2 spaces** (no tabs)
- Maximum line length: **120 characters** (soft guideline)
- No trailing whitespace
- One blank line between major CSS rule blocks

### CSS

```css
/* ✅ Good — descriptive comment headers */
/* ── METRICS ── */
.metric {
  background: rgba(13,33,72,0.5);
  border-radius: var(--radius-md);
  padding: 18px;
}

/* ❌ Avoid — magic numbers without context */
.metric {
  background: #0d2148;
  border-radius: 16px;
}
```

- Use **CSS variables** for all colors and radii (defined in `:root`)
- New colors must be added to `:root` before use — do not hardcode hex values in rules
- Animations should be **CSS-only** where possible (no JS animation libraries)
- Keep `z-index` values in the single digits where possible; comment any exception

### HTML

```html
<!-- ✅ Good — semantic sections with comment labels -->
<!-- ── NETWORK PULSE + FEED ── -->
<section class="section-grid">

<!-- ❌ Avoid — unlabelled div soup -->
<div>
  <div>
    <div>
```

- Use semantic HTML (`<section>`, `<article>`, `<nav>`, `<main>`) where appropriate
- Every major section should have a `<!-- ── SECTION NAME ── -->` comment above it
- IDs are for JavaScript hooks only; use classes for styling

### JavaScript

```javascript
// ✅ Good — explicit, descriptive
async function fetchNetwork(url) {
  const [block, gas, chainId] = await Promise.all([
    rpcCall(url, 'eth_blockNumber'),
    rpcCall(url, 'eth_gasPrice'),
    rpcCall(url, 'net_version')
  ]);
  return {
    block: hexToInt(block).toLocaleString(),
    gas: `${weiToGwei(gas)} gwei`,
    chainId
  };
}

// ❌ Avoid — compressed, unclear
const fetch=async u=>{const[b,g,c]=await Promise.all([rpcCall(u,'eth_blockNumber'),rpcCall(u,'eth_gasPrice'),rpcCall(u,'net_version')]);return{block:parseInt(b,16).toLocaleString(),gas:`${(parseInt(g,16)/1e9).toFixed(2)} gwei`,chainId:c}};
```

- Use `async/await`, not `.then()` chains
- All RPC calls must go through `rpcCall()` — do not `fetch()` directly
- Error handling: every `async` function that touches the network must have a `try/catch`
- Prefer `const` over `let`; never use `var`
- Function names should be verbs: `fetchNetwork`, `setLoaded`, `refresh`

---

## Commit Message Convention

This project follows [Conventional Commits](https://www.conventionalcommits.org/).

### Format

```
<type>(<optional scope>): <short description>

[optional body]

[optional footer(s)]
```

### Types

| Type | When to use |
|---|---|
| `feat` | A new feature or visible enhancement |
| `fix` | A bug fix |
| `docs` | Documentation only (README, comments, etc.) |
| `style` | CSS/visual changes with no logic impact |
| `refactor` | Code restructure with no feature/bug change |
| `perf` | Performance improvement |
| `chore` | Build tooling, CI, dependency changes |
| `test` | Adding or updating tests |

### Examples

```bash
# Feature
git commit -m "feat(metrics): add gas price sparkline for last 10 readings"

# Bug fix
git commit -m "fix(rpc): handle timeout gracefully on testnet endpoint"

# Documentation
git commit -m "docs: add CUSTOMIZATION guide for RPC configuration"

# Style
git commit -m "style(mobile): improve metric card layout on small screens"

# Breaking change (include ! and footer)
git commit -m "feat!: replace inline CSS with external stylesheet

BREAKING CHANGE: the project is no longer a single file.
See docs/MIGRATION.md for update instructions."
```

### Rules

- Subject line: max **72 characters**, lowercase, no period at the end
- Use the imperative mood: "add feature" not "added feature" or "adds feature"
- Body (if present): wrap at **72 characters**, explain *why* not *what*
- Reference issues: `Closes #12` or `Fixes #34` in the footer

---

## Pull Request Process

1. **Open a PR against `main`** — not any other branch unless a maintainer asked you to
2. **Fill out the PR template** completely — incomplete PRs may be closed without review
3. **Link related issues** — use `Closes #N` in the PR description to auto-close on merge
4. **Keep PRs focused** — one feature or fix per PR; avoid combining unrelated changes
5. **Screenshot your changes** — for any visual/CSS change, include a before/after screenshot in the PR
6. **Respond to review comments** within a reasonable time — PRs inactive for 30 days may be closed

### PR Checklist

Before marking your PR as ready for review:

- [ ] I have tested the change in at least one browser (Chrome, Firefox, or Safari)
- [ ] The file still opens cleanly with no console errors
- [ ] RPC reads still function after my change
- [ ] I have followed the code style guide
- [ ] I have used conventional commit messages
- [ ] I have updated documentation if my change affects usage or configuration
- [ ] My change does not introduce any `var` declarations, inline styles, or magic numbers
- [ ] I have not added external dependencies (no npm, no CDN scripts beyond Google Fonts)

---

## Design Principles

Keep these in mind when building features:

| Principle | What it means |
|---|---|
| **Zero dependency** | No npm packages, no CDN scripts (Google Fonts is the only external resource) |
| **No wallet** | The page must be fully functional with no wallet connection prompt |
| **Public data only** | Only read from public, unauthenticated RPC endpoints |
| **Single file** | The deployable artifact is one HTML file — keep it that way unless there is a compelling reason |
| **Honest data** | Never fake or mock live data — if the RPC fails, say so clearly |
| **Builder-first** | Design for developers and researchers, not general consumers |
| **Ocean theme integrity** | New UI elements should fit the deep-sea lighthouse aesthetic — no lime greens or pastels |

---

Thank you for contributing to Pharos Alpha. 🌊⚓

*The lighthouse is lit. Set sail.*
