# MemexLab — Documentation

The operating manual for an Obsidian-first, markdown-native, AI-assisted second brain built for strategic research, decision support, and long-term knowledge compounding.

This repository of documents is the source of truth. If a behaviour is not documented here, it is not part of the system.

## How to read these docs

Three reading paths, depending on who you are today.

**New user (one hour).** Read `00-overview.md`, then `quickstart.md`, then `09-onboarding.md`. That is enough to set up a vault, capture your first source, and generate your first output.

**Daily operator (half a day).** Add `04-daily-workflow.md`, `05-templates.md`, `06-metadata-and-tagging.md`, and `one-pager.md` to the above. Keep `maintenance-checklist.md` open on a second monitor during your weekly review.

**System owner / extender (full tour).** Read every file in numerical order, then revisit `07-automation.md` and `12-maintenance.md` whenever you change the engine.

## File map

| File                         | What it covers                                              |
| ---------------------------- | ----------------------------------------------------------- |
| `00-overview.md`             | What the system is, why it exists, design philosophy        |
| `01-architecture.md`         | Vault layers, engine, information flow                      |
| `02-core-concepts.md`        | Every term with a precise definition                        |
| `03-folder-structure.md`     | Per-folder purpose, rules, naming                           |
| `04-daily-workflow.md`       | Capture → ingest → compile → link → output                  |
| `05-templates.md`            | Source article, paper, concept, person, company, project, memo, slides, daily note |
| `06-metadata-and-tagging.md` | Frontmatter schema, tag taxonomy, linking rules             |
| `07-automation.md`           | CLI modes, scripts, how LLMs touch the vault                |
| `08-user-modes.md`           | Beginner / researcher / founder / operator / collaborator   |
| `09-onboarding.md`           | Step-by-step setup for a new user                           |
| `10-best-practices.md`       | How to keep the system clean                                |
| `11-common-mistakes.md`      | Failure modes and their fixes                               |
| `12-maintenance.md`          | Weekly / monthly / quarterly cadence                        |
| `13-future-expansion.md`     | Multi-user, API, agents, productisation                     |
| `14-faq.md`                  | Practical questions                                         |
| `quickstart.md`              | Ten-minute setup                                            |
| `one-pager.md`               | The whole system on a single page                           |
| `maintenance-checklist.md`   | Literal checklist, by cadence                               |
| `glossary.md`                | Alphabetical definitions                                    |

## Recommended repository layout

Your personal Memex lives across three top-level concerns — keep them in one repository so they version together.

```
memexlab/
  <your-vault>/           # The Obsidian vault (human-facing)
    <your-name>.md     # Persona (core note, root)
    memexlab.md      # Homepage (core note, root)
    inbox/               # Raw capture, unprocessed
    raw/                 # Ingested sources, pre-compile
    wiki/                # Canonical atomic notes
    people/              # Curated ontology — people
    companies/           # Curated ontology — companies
    philosophies/        # Curated ontology — stances
    projects/            # Active projects (each folder = one project)
    _qa/                 # Q&A outputs
    _lint/               # Lint reports
    _index/              # Structured index notes
    _essays/             # Essay outputs
    _slides/             # Slides outputs
    _charts/             # Chart PNGs + sidecar notes
    archive/             # Retired or deprecated content
    templates/           # Obsidian Templater templates
    .obsidian/           # Workspace config
    .memex/              # Engine state: snapshots, log.jsonl

  memex/                 # The CLI engine (this repo's code)
    memex/
    tests/
    scripts/
    prompts/
    pyproject.toml

  docs/                  # You are here
    README.md
    00-overview.md
    ...
```

Only the CLI engine lives under version control with git. The vault is backed up separately (Obsidian Sync, iCloud, tarball snapshots, etc.) — see `12-maintenance.md`.

## Recommended vault README structure

The vault itself should ship with a short README at its root so the system is self-describing even if you open it from a different device. A template lives at `templates/vault-README.md` and the generated file lives at `<vault>/README.md`:

```
# Latticework

Personal Memex vault for <owner>. See memexlab/docs for the full operating manual.

## Folders
<short purpose statement per folder>

## Daily commands
memex doctor       # sanity check
memex compile X    # cut a source into atomic notes
memex lint         # vault health report
memex qa "…"       # answer from vault
memex index "…"    # structured overview
memex export essay/slides "…"
memex chart <kind>

## Quality bar
<short summary — full rules in docs/10-best-practices.md>
```

## Conventions used in these docs

**Callouts.** Blocks labelled _Do this_ / _Do not do this_ / _Example_ / _Why it matters_ appear where the default behaviour is easy to get wrong. They are meant to be skimmed.

**Command samples.** Commands describe the intended `memex` CLI interface against a vault set up via `09-onboarding.md`. The engine that runs them is a separate, not-yet-public repository, so treat the samples as **conceptual until its release** rather than clone-and-run from this docs repo.

**Sample notes.** Sample frontmatter is valid against the current schemas in `memex/memex/schemas.py`. Sample bodies are deliberately short; production notes will be longer.

**Tone.** Calm, precise, and unapologetically opinionated where opinion matters. The system works because the rules are narrow; loosening them is a downgrade.
