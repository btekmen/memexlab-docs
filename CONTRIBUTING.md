# Contributing to MemexLab docs

This repository holds the **documentation and specification** for MemexLab. Improvements to
clarity, accuracy, examples, and structure are welcome.

> The `memex` engine lives in a separate, not-yet-public repository. Issues about engine
> behavior or installation can't be resolved here yet — this repo is docs only. See the
> [Preview status](README.md#preview-status--specified-vs-implemented).

## How to contribute

1. Open an issue describing the change (typo, unclear section, broken link, missing detail).
2. For edits, open a pull request against `main`.
3. Keep PRs focused and explain the "why" in the description.

## Guidelines

- **Accuracy over polish.** Don't describe capabilities as shipped if they're specified-only.
  Mark conceptual/engine-dependent steps as such.
- **No private data.** Never add real names, emails, company-internal material, vault
  contents, secrets, or anyone's personal data. Use the placeholders already in use
  (`<your-name>`, `<your-company>`, `<your-product>`, `<your-vault>`).
- **No hype.** Avoid "revolutionary / ultimate / 10x." Prefer precise, concrete language.
- **Respect the naming.** "MemexLab" is the project; `memex` is the engine/CLI. See the
  [repository map](README.md#repository-map).
- **Links must resolve.** Internal links are checked in CI (see `.github/workflows/docs-check.yml`).

## Checks

CI runs an internal-link check (lychee, offline) and an advisory markdown lint on every PR.
Run a quick local link sanity check before pushing if you like:

```bash
# any local markdown link checker, e.g. lychee:
lychee --offline "**/*.md"
```

Thanks for helping keep the docs honest and clear.
