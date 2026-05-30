# MemexLab — Documentation

The operating manual for **MemexLab**, a local-first, markdown-native knowledge operating
system for strategic learning, synthesis, and decision support — designed to be operated
by an AI agent through explicit skills, schemas, evals, and governance.

> **Status: documentation preview.** This repository is the **specification and operating
> manual** for MemexLab. The engine (`memex` CLI) and an example vault are **separate and
> not yet public**, so the command samples and quickstart here are **conceptual until the
> engine is released** — this is not yet a "clone this and run it" repo. See
> [Preview status](#preview-status--specified-vs-implemented) for what's implemented vs specified.

## Repository map

A reader will encounter a few related names — here's what each is:

| Name | What it is | Visibility |
| --- | --- | --- |
| **`memexlab-docs`** (this repo) | Documentation & specification | Public |
| **`memexlab`** | The website at [memexlab.xyz](https://memexlab.xyz) | Public |
| **`memex`** | The CLI engine + skills / schemas / evals / governance | Private — not yet released |
| Personal vaults | Your actual knowledge base | Never published |

**MemexLab** is the project/brand; **`memex`** is the engine (a Python CLI). Your vault data
stays local and private — the framework is public-ready, your knowledge base is not.

## Agent stack

MemexLab is **provider-agnostic**: the vault is plain markdown operated by a CLI, so any
capable LLM can run the model-driven steps. The reference implementation targets
**OpenClaw-compatible agents** as the runtime/skills surface, and the LLM integration is
isolated in a single client — point it at **any provider (Anthropic, OpenAI, …)** by setting
`ANTHROPIC_API_KEY` or `OPENAI_API_KEY`. You can change provider without changing the vault,
and the deterministic modes (lint, chart, retrieval) use no model at all.

## Core idea

- **Markdown is the human-readable compiled layer.** People can inspect, edit, diff, and own the knowledge base.
- **Sources preserve evidence.** Raw or lightly cleaned inputs stay traceable.
- **Items capture judgment.** Synthesized notes should contain a thesis, reusable framing, or decision-relevant idea.
- **The database is the machine layer.** Embeddings, search indexes, graph edges, and eval traces accelerate retrieval but do not replace the vault.
- **Agents must cite.** Answers should point back to source notes, entity slugs, and provenance.
- **Benchmarks beat vibes.** Retrieval quality, citation quality, deduplication, and contradiction handling must be measured over time.
- **Harness quality sets reliability.** Execution, tools, context, lifecycle, observability, verification, and governance are first-class system layers.

> "The filesystem is the database. Plain markdown is the storage. Obsidian is the editor. A Python CLI (`memex`) is the engine. No cloud. No lock-in."

## Operating thesis

> As execution becomes commoditized, cognition becomes leveraged, but deep understanding becomes the scarce asset.
>
> You can outsource your thinking, but you cannot outsource your understanding.

Source: https://x.com/yacinemtb/status/2018886083120153046?s=46&t=JrHmNURN3558ApZxbKYavg

## Purpose

Memex exists to help answer a simple question:

> What do we know, what does it mean, and how should it change our judgment?

- **Project site:** <https://memexlab.xyz>
- **Showcase:** <https://memexlab.xyz/showcase.html>
- **Status:** `0.2.0-harness-preview` (early preview — not production-stable)

These docs are reference material. Paths like `~/Documents/Obsidian/<your-vault>/` are
illustrative — substitute your own vault path. Examples use generic placeholders
(`<your-name>`, `<your-company>`, `<your-product>`); adapt them to your own domains.

## Start here

If you're **new to the system**, read in order:

1. [`docs/quickstart.md`](docs/quickstart.md) — the compressed setup walkthrough (conceptual until the engine ships).
2. [`docs/one-pager.md`](docs/one-pager.md) — the whole system on one page.
3. [`docs/00-overview.md`](docs/00-overview.md) — what MemexLab is and why.

If you're **setting up for real**:

- [`docs/09-onboarding.md`](docs/09-onboarding.md) — complete step-by-step setup.
- [`docs/03-folder-structure.md`](docs/03-folder-structure.md) — what goes where.
- [`docs/05-templates.md`](docs/05-templates.md) — the Obsidian templates you need.

If you're **already operating**:

- [`docs/04-daily-workflow.md`](docs/04-daily-workflow.md) — the daily / weekly rhythm.
- [`docs/10-best-practices.md`](docs/10-best-practices.md) — what to do.
- [`docs/11-common-mistakes.md`](docs/11-common-mistakes.md) — what to avoid.
- [`docs/12-maintenance.md`](docs/12-maintenance.md) — weekly → yearly cadence.
- [`docs/maintenance-checklist.md`](docs/maintenance-checklist.md) — checklists by cadence.

## Full index

| File | Section |
| --- | --- |
| [`docs/00-overview.md`](docs/00-overview.md) | 1. Overview |
| [`docs/01-architecture.md`](docs/01-architecture.md) | 2. Architecture |
| [`docs/02-core-concepts.md`](docs/02-core-concepts.md) | 3. Core concepts |
| [`docs/03-folder-structure.md`](docs/03-folder-structure.md) | 4. Folder structure |
| [`docs/04-daily-workflow.md`](docs/04-daily-workflow.md) | 5. Daily workflow |
| [`docs/05-templates.md`](docs/05-templates.md) | 6. Templates and note types |
| [`docs/06-metadata-and-tagging.md`](docs/06-metadata-and-tagging.md) | 7. Metadata and tagging rules |
| [`docs/07-automation.md`](docs/07-automation.md) | 8. Automation and scripts |
| [`docs/08-user-modes.md`](docs/08-user-modes.md) | 9. User modes |
| [`docs/09-onboarding.md`](docs/09-onboarding.md) | 10. Onboarding guide |
| [`docs/10-best-practices.md`](docs/10-best-practices.md) | 11. Best practices |
| [`docs/11-common-mistakes.md`](docs/11-common-mistakes.md) | 12. Common mistakes |
| [`docs/12-maintenance.md`](docs/12-maintenance.md) | 13. Maintenance |
| [`docs/13-future-expansion.md`](docs/13-future-expansion.md) | 14. Future expansion |
| [`docs/14-faq.md`](docs/14-faq.md) | 15. FAQ |
| [`docs/quickstart.md`](docs/quickstart.md) | Ten-minute setup |
| [`docs/one-pager.md`](docs/one-pager.md) | Whole system on one page |
| [`docs/maintenance-checklist.md`](docs/maintenance-checklist.md) | Checklists by cadence |
| [`docs/glossary.md`](docs/glossary.md) | Alphabetical glossary |

## Lineage and credits

Primary intellectual credit goes to Andrej Karpathy's **LLM Knowledge Bases** thread and **LLM Wiki** gist. Karpathy's core pattern is the foundation: raw sources remain immutable, the LLM incrementally maintains a persistent markdown wiki, and useful answers can be filed back into the wiki so knowledge compounds instead of being re-derived from scratch.

Karpathy explicitly connects the idea back to Vannevar Bush's **Memex** (1945): a personal, curated knowledge store built around associative trails between documents. Bush's vision was closer to this project than to what the web became: private, actively curated, and structured around connections that are as valuable as the documents themselves. The missing maintenance layer is what the LLM now supplies.

This repository extends that pattern into an agent-operable Memex framework with schemas, skills, evals, governance, validation, and a public/private vault boundary.

Thank you to Garry Tan for developing and sharing both GStack and GBrain. They are major references for the agent-workflow and brain-layer parts of this project.

Important adjacent influences:

- Andrej Karpathy, **LLM Knowledge Bases**: https://x.com/karpathy/status/2039805659525644595
- Andrej Karpathy, **LLM Wiki** gist: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
- Garry Tan, **GStack**: https://github.com/garrytan/gstack
- Garry Tan, **GBrain**: https://github.com/garrytan/gbrain/tree/master

## Preview status — specified vs implemented

This repo is the **specification** (prose docs). The **executable layer lives elsewhere**
and is not yet public, so treat commands and the quickstart as the intended interface,
not a clone-and-run experience from this repo.

| Capability | In this repo | Status |
| --- | --- | --- |
| Operating model, schemas, taxonomy, workflows | Specified (docs) | ✅ documented |
| `memex` CLI (`compile`, `qa`, `lint`, `index`, `export`, `chart`) | Described, not included | 🔜 engine repo (private) |
| Skills / schemas / evals / governance files | Described, not included | 🔜 engine repo (private) |
| Example vault | Referenced | 🔜 separate release |
| Public install path | Planned | 🔜 follow [memexlab.xyz](https://memexlab.xyz) |

## Scope

This repository is **documentation only**. The engine (`memex`) and any real vault live
separately, and private vault data is never published — the framework is public-ready,
your knowledge base is not.

## License

Licensed under the [MIT License](LICENSE).
