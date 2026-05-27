[✦ ShadoLogiq Labs](https://shadologiq.com) · [Org profile](https://github.com/shadologiq-labs) · **Contributing** · [Code of Conduct](CODE_OF_CONDUCT.md) · [Security](SECURITY.md) · [Support](SUPPORT.md)

---

# Contributing to ShadoLogiq Labs

We don't file tickets — we rewrite the logic. If a platform is slowing you down and you've got an idea (or a patch), this is the place.

---

## Before you start

Each repo has its own architecture and conventions. **Read its `README.md` and `CLAUDE.md` first** — they describe what's there, why it's structured that way, and which decisions are load-bearing.

## House rules

These apply to every project under ShadoLogiq Labs.

### 1. No runtime dependencies (default)

Vanilla JavaScript + browser APIs. If you think you need a runtime dependency, open an issue first — the answer is usually "no, here's how to do it without one."

Build-time / dev-only dependencies are fine in `devDependencies`.

### 2. Local-only, zero telemetry

Nothing we ship phones home. No analytics SDKs, no error reporting services, no usage pings. If you add code that talks to a server we don't run, the PR will be rejected on principle.

### 3. Open an issue first for anything non-trivial

Spec out the change. Mention the platform / user pain you're solving. This saves both of us time if the direction is wrong.

### 4. One concern per PR

Don't bundle a refactor with a bugfix with a docs update. Three PRs > one mega-PR.

### 5. Imperative commit messages, with the *why*

- ✅ `Fix linker panel re-render loop on ServiceNow form save`
- ❌ `fixes`

### 6. Test what you can

- Pure logic → unit tests required
- DOM interactions → manual reproduction steps in the PR description
- Browser extensions → tested on each target (Chrome / Firefox / Edge)
- Embed widgets → tested at the documented breakpoints

### 7. Run `npm run check` (or the project's equivalent) before pushing

Lint + validate + test. CI runs the same thing; save the round-trip.

---

## PR template

```markdown
## Summary
One sentence about what this does.

## Why
The user pain or upstream behavior this addresses.

## Changes
- Bullet points
- Of what changed

## Testing
- [ ] Ran `npm run check`
- [ ] Manually tested on [Chrome / Firefox / Edge / live site / ServiceNow instance]
- [ ] No regressions in adjacent features

## Screenshots / demo
(If UI changed.)
```

---

## Code style

### JavaScript
- ES2022+. No transpilation.
- Clear names over clever names. `recordId`, not `rid`.
- Comments only where the *why* isn't obvious from the code.
- No comments that restate what the code says.

### HTML / CSS
- Semantic HTML. Real headings, real labels.
- CSS custom properties over hardcoded values.
- Mobile-first responsive breakpoints.

### Manifests / configs
- Keep Chrome and Firefox manifests in sync when adding permissions.
- Bump version in `package.json` *and* manifests together.

---

## Project-specific guidance

### SNapp Extension
- Dual manifests (`manifest.chrome.json`, `manifest.firefox.json`) — sync them when adding permissions or content scripts.
- Test on a real ServiceNow instance — mocks miss too much.
- No telemetry, ever. Privacy-first is the whole point.
- Content script timing: `document_idle` and frame execution matter.

### Gapps Embed
- **No build step.** All files must be drop-in usable as-is.
- Self-hosting must keep working — anyone should be able to fork, edit `apps.js`, and serve statically.
- Test the three breakpoints: ≥1024px / 600–1023px / <600px.
- Cache behavior matters — GitHub Pages serves with HTTP/2 multiplexing and long cache lifetimes; respect that.

---

## What we won't merge

- Anything that adds telemetry, analytics, or external API calls (unless they're the user's own opt-in)
- Anything that adds a runtime dependency without prior discussion
- Anything monetized — ads, "premium" features, paid tiers
- Bundled refactors-plus-features-plus-bugfixes in one PR
- Code without a clear *why*

## What we'll happily merge

- Bugfixes with reproduction steps
- New features that match the project's scope (check the README's "what this does")
- Docs improvements
- Tests for code that doesn't have them yet
- Performance wins with before/after measurements
- Accessibility improvements

---

## Getting help

- Stuck on the codebase? Open a discussion or issue — `question` label is fine.
- Want feedback on an idea before coding? Open an issue first.
- Found a security issue? Use [SECURITY.md](./SECURITY.md), not a public issue.

---

If you've made it this far, you probably get it. Welcome.

---

[✦ ShadoLogiq Labs](https://shadologiq.com) · [Org profile](https://github.com/shadologiq-labs) · **Contributing** · [Code of Conduct](CODE_OF_CONDUCT.md) · [Security](SECURITY.md) · [Support](SUPPORT.md)
