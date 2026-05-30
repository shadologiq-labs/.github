[✦ ShadoLogiq Labs](https://shadologiq.com) · [Org profile](https://github.com/shadologiq-labs) · [Ethos](ETHOS.md) · [Contributing](CONTRIBUTING.md) · [Code of Conduct](CODE_OF_CONDUCT.md) · **Security** · [Support](SUPPORT.md)

---

# Security policy

ShadoLogiq Labs ships code that runs in your browser, on your machine. Privacy and security are foundational — not features.

If you find a vulnerability, please report it responsibly.

---

## How to report

**Don't open a public issue.** Use GitHub's [**private vulnerability reporting**](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability) on the affected repo — that's the only supported channel. Look for the *Security* tab on the repo, then *Report a vulnerability*.

Why this channel? It's end-to-end encrypted, creates a private draft advisory we can collaborate on, and keeps the disclosure timeline coordinated between you and us.

Include:

- **Which project / repo** is affected
- **The vulnerability** — what it is and what it lets an attacker do
- **Reproduction steps** — how to trigger it
- **Suggested fix** if you have one
- **Whether you'd like credit** when we publish the advisory (default: yes, with your name; you can request anonymity)

We acknowledge reports within **24 hours** and work with you on a fix and disclosure timeline.

---

## What we care about per project

### SNapp Extension
The extension reads ServiceNow form fields and writes to the clipboard. The threat model includes:

- Leaking sensitive record data (description, CI info, user names) to anywhere outside the active tab
- Misusing a granted permission beyond its documented scope
- Code injection via crafted ServiceNow form content
- Cross-frame data exfiltration

**Privacy guarantees we maintain:**
- All processing happens in the page context
- No network calls outside the page
- No telemetry
- Storage is local-only (`chrome.storage.local`), never synced

### Gapps Embed
Static iframe content with query-string and `postMessage` configuration. The threat model includes:

- CSS injection via theme query parameters
- Redirection via the `domain` parameter (Workspace AccountChooser rewrite)
- Sprite or data manipulation by a malicious fork
- Iframe sandboxing bypasses via crafted `postMessage` payloads

**Mitigations in place:**
- Color params validated against a strict hex pattern before being set as CSS variables
- Domain params validated against a well-formed-hostname regex
- App/category keys validated against `^[a-z0-9-]+$`
- `postMessage` listener only accepts `type: 'gapps-embed-theme'` and ignores any other shape
- No `eval`, no `innerHTML` with untrusted input, no dynamic script loading

---

## Supported versions

The **latest minor version** receives security fixes. Older versions get fixes only if they're being actively used by known consumers and the fix is straightforward.

Patches ship as version bumps (`v1.0.1`, `v1.1.2`, etc.) and are announced via GitHub Releases and a published security advisory.

---

## What we'll do

1. Confirm the vulnerability within 24 hours of receipt
2. Develop and test a fix
3. Coordinate disclosure timing with you
4. Release a patch
5. Publish a GitHub Security Advisory
6. Credit you (or honor anonymity if you prefer)

---

ShadoLogiq Labs runs on the client. That puts security in our hands and yours. Thanks for helping us keep it tight.

---

[✦ ShadoLogiq Labs](https://shadologiq.com) · [Org profile](https://github.com/shadologiq-labs) · [Ethos](ETHOS.md) · [Contributing](CONTRIBUTING.md) · [Code of Conduct](CODE_OF_CONDUCT.md) · **Security** · [Support](SUPPORT.md)
