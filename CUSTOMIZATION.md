# Customization Guide

How to adapt Pharos Alpha for your own use case.

---

## Changing Colors

All colors are CSS custom properties. Edit the `:root` block at the top of the `<style>` tag:

```css
:root {
  --teal:  #00b4d8;   /* ← primary accent: change this to your brand color */
  --foam:  #90e0ef;   /* ← heading color */
  --white: #e8f4ff;   /* ← body text */
}
```

To switch to a different accent color, change `--teal`, `--teal-dim`, and `--glow` together.

---

## Changing RPC Endpoints

Edit the `endpoints` object in the `<script>` block:

```javascript
const endpoints = {
  mainnet: 'https://rpc.pharos.xyz',           // ← swap for any EVM-compatible RPC
  testnet: 'https://atlantic.dplabs-internal.com'
};
```

Both must be EVM-compatible JSON-RPC 2.0 endpoints that respond to `eth_blockNumber`, `eth_gasPrice`, and `net_version`.

---

## Changing the Refresh Rate

```javascript
setInterval(refresh, 20000);  // 20000ms = 20 seconds
```

- `5000` = 5 seconds (aggressive — be mindful of public endpoint rate limits)
- `60000` = 1 minute (conservative)
- `0` to disable auto-refresh entirely and remove this line

---

## Adding Your Own Branding

### Brand Name (Topbar)

```html
<div class="brand">
  <!-- ... mini lighthouse SVG ... -->
  Pharos Alpha  <!-- ← change this text -->
</div>
```

### Signature Footer

```html
<div class="signature-inner">
  <div class="dot"></div>
  Made with 🌊 for the Pharos Ecosystem  <!-- ← change this -->
  <span style="color:var(--teal);">By Kennyy</span>  <!-- ← and this -->
  <div class="dot"></div>
</div>
```

---

## Deploying

The project is a single HTML file. Deploy it anywhere:

```bash
# Vercel
vercel --prod src/

# Netlify (CLI)
netlify deploy --prod --dir src/

# GitHub Pages
# Enable Pages in repo settings → set source to main branch root
# Copy pharos_alpha.html to index.html

# IPFS
ipfs add src/pharos_alpha.html

# Any static host
# Just upload the .html file. That's it.
```
