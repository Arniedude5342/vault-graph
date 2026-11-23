# Using vault-graph with Claude Code (or any shell-capable agent)

The point of the tool is to stop the agent from reading whole notes. The agent asks the graph first,
then opens only the section it was pointed to.

## 1. Add a rule to `CLAUDE.md`

Put this at the top of the `CLAUDE.md` in your vault root:

```markdown
## Vault graph (read first)

Before opening notes or grepping, query the graph from the vault root:

- `vault-graph search "question"` finds notes and sections that answer it.
- `vault-graph note "Name"` shows the outline with line ranges. Open only what you need with
  `vault-graph section "Name" "Heading"`.
- A note over ~3k tokens is never read whole: use `section`.
- To append to a note, run `vault-graph section "Name" "Heading" --tail 3 --numbers` and edit after that line.
- To check whether a note exists before creating one: `vault-graph note "Name" --exact` (exit code 4 = no).
- Open tasks: `vault-graph tasks --match <area>` (also `--overdue`, `--until +7`).
- The index refreshes itself on every command. Never edit anything inside `.vault-graph/`.
```

If you installed it as a plain script instead of a command, use
`python /path/to/vault_graph.py --vault . ...` in place of `vault-graph`.

## 2. Optional: install it as a skill

Copy [`skills/vault-graph/SKILL.md`](../skills/vault-graph/SKILL.md) to `.claude/skills/vault-graph/SKILL.md`
in your vault (or `~/.claude/skills/vault-graph/` for all projects). Claude Code then loads the
instructions on demand instead of carrying them in every conversation.

## 3. Keep the cache out of sync tools and git

The cache folder (`.vault-graph/`) is derived data. Add it to `.gitignore`, and to your sync tool's
ignore list if it fights over many small files.

## Why this saves tokens

| Without the graph | With the graph |
|---|---|
| Read a 5k-token note to find one paragraph | `section` returns the ~100-token section |
| Grep, then open 5 files to see which one matters | `search` ranks them and names the section |
| Read the task list file to find this week's items | `tasks --until +7` returns only those lines |
| Re-read the folder tree every conversation | `report` is a one-screen overview |
