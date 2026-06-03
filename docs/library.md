# Library

The [`library/`](https://github.com/btekmen/memexlab-engine/tree/main/library) in the public
engine repository is a growing collection of **knowledge assets** — synthesized notes distilled
from papers, reports, and books, each with provenance, key ideas, and atomic-note candidates. It
is the durable output the system exists to produce: read something, turn it into a citable asset,
let it compound.

It is organized by type, and a generated index keeps the catalogue current:

| Group | Examples |
| --- | --- |
| `papers/` | *Attention Is All You Need* (Vaswani et al., 2017) |
| `reports/` | *AI eats the world* (Benedict Evans, 2026) |
| `books/` | *Skunk Works*, *Grace Hopper*, *The Art of Doing Science and Engineering* |

The always-current list lives in the generated index:
[`library/README.md`](https://github.com/btekmen/memexlab-engine/blob/main/library/README.md).

## Add an asset

1. Drop a markdown file into `library/papers/`, `library/reports/`, or `library/books/` with
   frontmatter (`type: source`, `title`, `author`/`authors`, `year`, `url`, `tags`).
2. Write a short summary, the key ideas, and `[[atomic note]]` candidates.
3. Regenerate the index: `python3 scripts/build_library_index.py`.

The index groups assets by type and lists title / author(s) / year — no manual editing.

Papers and reports link to their canonical source (arXiv, the author's site) rather than
bundling the PDF: the asset is the *distilled* knowledge, not a copy of the source.
