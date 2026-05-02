# Security Policy

## Supported Versions

| Version | Supported |
|---|---|
| 1.1.x | ✅ Yes |
| 1.0.x | ⚠️ Best-effort |
| < 1.0 | ❌ No |

## Scope

Pharos Alpha is a **read-only, client-side, static HTML file**. It:

- Makes outbound requests to **public Pharos RPC endpoints only**
- Does **not** handle any user authentication, sessions, or private keys
- Does **not** store any user data
- Does **not** have a backend, server, or database

The attack surface is therefore narrow. However, we still take security seriously and welcome responsible disclosure.

## What to Report

**In-scope issues:**

- Cross-Site Scripting (XSS) via dynamically rendered RPC response data
- Malicious RPC endpoint injection through URL parameters (if ever added)
- Content Security Policy gaps
- Subresource integrity issues with external fonts

**Out-of-scope:**

- Vulnerabilities in the Pharos Network itself — report those to the [Pharos team](https://pharos.xyz)
- Vulnerabilities in public RPC endpoints — report those to the [Pharos team](https://pharos.xyz)
- Self-XSS (requires a user to attack themselves)
- Phishing via domain lookalikes (not our domain)
- Issues in third-party services we link to

## Reporting a Vulnerability

**Do not open a public GitHub issue for security vulnerabilities.**

Please report security issues privately. You can:

1. Use [GitHub's private vulnerability reporting](https://github.com/kennyy/pharos-alpha/security/advisories/new) (preferred)
2. Email the maintainer directly (listed on the GitHub profile)

**Include in your report:**
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if you have one)

We will acknowledge your report within **48 hours** and aim to release a fix within **7 days** for critical issues.

## Responsible Disclosure

We follow responsible disclosure practices:

- We will work with you to understand and validate the issue
- We will credit you in the fix commit and CHANGELOG (unless you prefer anonymity)
- We ask that you give us reasonable time to fix before public disclosure
- We will not take legal action against researchers acting in good faith

Thank you for helping keep the Pharos community safe. 🌊
