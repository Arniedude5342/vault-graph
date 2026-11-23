---
name: vault-graph
description: Query a Markdown/Obsidian vault through a local graph before opening notes. Use whenever you need to find, read or update notes, tasks or links in the vault, so only the relevant section is read instead of whole notes.
---

# vault-graph

Run from the vault root. The index updates itself; no LLM is involved and notes are never modified.

## Workflow

1. **Find**: `vault-graph search "question"`. It lists notes, matching sections with line ranges, and a
   few excerpts. Often the excerpt is already the answer.
2. **Outline** (only if needed): `vault-graph note "Name"` shows headings with line ranges and sizes.
3. **Read**: `vault-graph section "Name" "Heading"`. Never read a note over ~3k tokens whole.
   Use `--lines A-B` for an exact range.
4. **Append to a note**: `vault-graph section "Name" "Heading" --tail 3 --numbers`, then insert after
   the last printed line.
5. **Does a note exist?** `vault-graph note "Name" --exact`: exit code 0 = yes, 4 = no, 3 = ambiguous.

## Other commands

- `vault-graph tasks [--match X] [--until tomorrow|+N|YYYY-MM-DD] [--overdue]` open tasks without
  opening the files that hold them.
- `vault-graph recent --days 7` and `vault-graph changed` what moved lately.
- `vault-graph path "A" "B"` how two notes connect.
- `vault-graph audit` broken links, duplicate names, bad frontmatter, orphans.
- `vault-graph report` overview with hubs, communities and the biggest notes.

## Rules

- Answers are cut at ~1,200 tokens. If a line says "cut by the budget", narrow the query or pass
  `--budget N` instead of reading files directly.
- If `vault-graph` is not on the PATH, use `python /path/to/vault_graph.py --vault .`.
- Never edit files inside `.vault-graph/`.
