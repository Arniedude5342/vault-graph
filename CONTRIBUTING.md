# Contributing

Thanks for considering a contribution. The project is small on purpose: one file, no dependencies.

## Ground rules

- Keep it standard-library only and compatible with Python 3.8+.
- Notes must never be modified by any command. A test enforces this.
- Add or update a test for every behaviour change: `python -m unittest discover -s tests -v`.
- If your change needs a new kind of note in the demo vault, add it to `examples/sample-vault` and
  update the expected counts in `tests/test_vault_graph.py`.

## Good first issues

- Parse standard Markdown links (`[text](note.md)`) as graph edges.
- Stop words and stemmers for more languages.
- A `--json` output mode for scripting.
- Index `#tags` and tasks written by the Obsidian Tasks plugin with more date formats.

Open an issue before starting anything large so we can agree on the approach.
