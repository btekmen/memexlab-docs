# Self-hosting the agent

MemexLab is local-first by design, and you can run it as a self-hosted agent today. The
public [`memexlab-engine`](https://github.com/btekmen/memexlab-engine) repository ships a
small, runnable reference agent under [`runner/`](https://github.com/btekmen/memexlab-engine/tree/main/runner)
that operates a markdown vault on your own machine.

## The four layers

A self-hosted agent is four layers, and each is provided:

| Layer | What it is | Provided by |
| --- | --- | --- |
| Workspace | the agent's working directory | a markdown vault (yours, or the bundled `examples/fake-vault`) |
| Capabilities | what the agent knows how to do | the Agent Skills in `skills/` |
| Runtime | the loop that reasons and calls tools | the reference `runner/`, or OpenClaw for the full surface |
| Model | the reasoning backend | local *or* hosted — one environment variable |

## Switchable backend

The reasoning backend flips on a single variable, `MEMEX_PROVIDER`. Local and hosted share
one code path because Ollama, vLLM, and LM Studio all expose an OpenAI-compatible endpoint, so
"self-hosted model" and "hosted API" differ by one flip, not a rewrite.

| `MEMEX_PROVIDER` | Backend | Requirements |
| --- | --- | --- |
| `anthropic` | Anthropic Messages API | `pip install anthropic`, `ANTHROPIC_API_KEY` |
| `openai` | OpenAI Chat Completions | `pip install openai`, `OPENAI_API_KEY` |
| `local` | Ollama / vLLM / LM Studio (air-gapped) | `pip install openai`, a running local server |

## Run it

```bash
# Load skills and the vault with no key and no model:
python3 runner/agent.py --dry-run --vault examples/fake-vault

# Then choose a backend and give it a task against your workspace:
export MEMEX_PROVIDER=local        # or anthropic | openai
python3 runner/agent.py --task "Summarize each note under people/" --vault ~/vault
```

## Pair with Obsidian

Point Obsidian at the same folder you pass to `--vault`. Edit and browse there; let the agent
ingest, link, and synthesize. The vault is plain markdown on disk, so both see the same files
with no sync layer between them.

## Reference runner vs. OpenClaw

The reference runner is intentionally minimal — a runtime-agnostic way to run the skills and a
zero-infrastructure local option. For the fuller agent surface (background daemon, MCP, broader
tooling), run [OpenClaw](https://github.com/openclaw/openclaw) against the same `skills/`. The
skills and the vault are identical either way.

Full guide: [Self-hosting the agent](https://btekmen.github.io/memexlab-engine/engineering/self-hosting/).
