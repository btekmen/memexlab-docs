# Quickstart

> **Conceptual until the engine ships.** This walkthrough describes the intended setup —
> roughly ten minutes once the `memex` engine is publicly available. The engine is a
> separate, not-yet-public repository, so the clone step below is a placeholder for now.
> See the repo's [Preview status](../README.md#preview-status--specified-vs-implemented).

A compressed path from zero to a working vault with one source ingested and one concept note created. The full onboarding is in `09-onboarding.md`; this page is the compressed version.

## Prerequisites (2 min)

Install:

```bash
brew install git python@3.12 obsidian
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Get an API key from your LLM provider — e.g. Anthropic (https://console.anthropic.com) or OpenAI (https://platform.openai.com) — and export the variable it expects:

```bash
echo "export ANTHROPIC_API_KEY=sk-ant-..." >> ~/.zshrc   # ...or OPENAI_API_KEY
source ~/.zshrc
```

## Clone the engine (1 min)

```bash
git clone <your-memex-repo> ~/memex
cd ~/memex
uv sync
```

## Create the vault (1 min)

```bash
mkdir -p ~/Documents/Obsidian/<your-vault>/{inbox,raw,wiki,people,companies,philosophies,eras,projects,archive,templates,_qa,_index,_essays,_slides,_charts,_lint,.memex/snapshots}
touch ~/Documents/Obsidian/<your-vault>/.memex/log.jsonl
echo "VAULT_PATH=$HOME/Documents/Obsidian/<your-vault>" > ~/memex/.env
```

Open the vault in Obsidian: `File → Open vault → Open folder as vault`, pick `~/Documents/Obsidian/<your-vault>`.

Install the **Templater** plugin from `Settings → Community plugins`. Point Templater's template folder at `templates/`.

## Confirm the engine sees the vault (1 min)

```bash
cd ~/memex
uv run python -m memex doctor --api
```

Expect `doctor_ok`. If not, read the error — it'll tell you exactly what to fix.

## Add the two core notes (2 min)

Create `~/Documents/Obsidian/<your-vault>/<your-name>.md`:

```markdown
---
title: "<your-name>"
type: persona
created: 2026-04-19
updated: 2026-04-19
status: active
tags: []
latticework: []
---

# <your-name>

Founder / operator in fintech. Building <your-company> and <your-product>. Thinks in terms
of five Latticework problems: seeing reality clearly, deciding under uncertainty,
allocating time and energy, avoiding self-deception, playing long games.
```

Create `~/Documents/Obsidian/<your-vault>/memexlab.md`:

```markdown
---
title: "MemexLab"
type: manifest
created: 2026-04-19
updated: 2026-04-19
status: active
tags: []
latticework: []
---

# MemexLab

A markdown-first second brain. Inbox → raw → wiki → outputs. Filesystem is the
database. Engine is additive. LLM compiles; human decides.
```

## Ingest one source (2 min)

Find a web article you want to keep. Create `~/Documents/Obsidian/<your-vault>/raw/2026-04-19-example-source.md`:

```markdown
---
title: "<article title>"
type: source
source_url: <url>
publisher: <publisher>
publication_date: 2026-04-17
ingested: 2026-04-19
status: seed
tags: [topic/<your-topic>]
latticework: [problem-1]
---

## Original text

<paste the article text here>

## Reactions

- <one sentence>

## Related

-
```

## Compile it (1 min)

```bash
uv run python -m memex compile \
    ~/Documents/Obsidian/<your-vault>/raw/2026-04-19-example-source.md
```

Read the dry-run output. If it looks right:

```bash
uv run python -m memex compile \
    ~/Documents/Obsidian/<your-vault>/raw/2026-04-19-example-source.md --apply
```

New files appear in `wiki/`. Open one in Obsidian; read it; add two `[[links]]` to related concepts.

## Ask the vault a question

```bash
uv run python -m memex qa "What did I just learn from the source?"
```

An answer note lands in `_qa/` with slug citations. Open it in Obsidian; follow the links back to the atomic notes.

## Schedule the daily linter

```bash
crontab -e
```

Add:

```cron
0 6 * * * cd ~/memex && uv run python scripts/lint_daily.py \
    2>> ~/Documents/Obsidian/<your-vault>/.memex/log.jsonl
```

From tomorrow morning, the vault lints itself.

## You're done

The loop is live. Capture aggressively; compile weekly; ask questions whenever you want; produce when you have a reason.

Read `04-daily-workflow.md` for the day-to-day rhythm, `10-best-practices.md` for how to keep the vault compounding, and `11-common-mistakes.md` for what to watch out for.
