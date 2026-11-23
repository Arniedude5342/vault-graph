# Changelog

## 0.1.0

First public release, extracted from a private tool used on a real 800-note vault.

- Commands: `search`, `note`, `section`, `tasks`, `recent`, `changed`, `path`, `audit`, `report`, `update`.
- Incremental, hash-based index; deterministic extraction; no LLM and no dependencies.
- Optional `config.json` (language, ignored and template folders, search weights, task scope, link and summary properties).
- English and Portuguese stop words and stemmers.
- Fixed: `update --force` now bypasses the "folder looks incomplete" guard, as its warning message says.
- Fixed: `update` reports its counts even when nothing changed.
- Frontmatter values that are not note names (for example `area: Finance`) are no longer reported as broken links.
