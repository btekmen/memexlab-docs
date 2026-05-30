# Security & privacy

This repository is **documentation only** — it contains no engine code, no servers, no
credentials, and no private vault data. There is no running service to attack here.

## Reporting

If you find something that shouldn't be public — a leaked secret, personal data, or
private vault content that slipped into these docs — please report it privately:

- Use **GitHub → Security → Report a vulnerability** (private advisory) on this repo, or
- Open an issue **without** including the sensitive content, and a maintainer will follow up.

Please do not open a public issue that itself reproduces the sensitive material.

## Scope & boundaries

- The **engine** (`memex`) and any real **vault** live in separate repositories. Private
  vault data is never published; the public/private boundary is part of the design.
- These docs use placeholders (`<your-name>`, `<your-company>`, `<your-product>`,
  `<your-vault>`) in place of any real identifiers.
- API keys belong in your shell environment only, never committed to any repository.

## Supported

This is a `0.2.0-harness-preview` documentation preview. There are no security guarantees
or supported versions yet; treat everything as pre-release.
