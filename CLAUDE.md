<!-- markdownlint-disable MD007 -- Unordered list indentation -->
<!-- markdownlint-disable MD010 -- No hard tabs -->
<!-- markdownlint-disable MD033 -- No inline html -->
<!-- markdownlint-disable MD055 -- Table pipe style [Expected: leading_and_trailing; Actual: leading_only; Missing trailing pipe] -->
<!-- markdownlint-disable MD041 -- First line in a file should be a top-level heading -->
# CLAUDE.md

Living project memory (state, dev/test workflow): @.claude/memory.md

## Clean-room (read first)

This is a clean-room GPLv2+ reimplementation of ZFS. This context is the IMPLEMENTATION side: never read OpenZFS source (no cat/Read/grep-with-content). The published 2006 on-disk spec is safe (it's a document). Post-2006 features come only via the spec pipeline. Full rules: `github/cleanroom.md`. Why it matters and current state: `.claude/memory.md`.

## Attribution (this project)

- `Instance:` here is always `zfs-gpl-implementation`. The spec environment uses `zfs-gpl-spec`.

- The remote is the SSH alias `git@github_t00mietum:...`, not literal `github.com`. `gh` is authed under my personal account; keep that account out of history and content.

## Build / run

- Rust workspace under `github/`. rustfmt pins `hard_tabs = true`, which keeps tab indentation rustfmt-canonical; don't remove it.

- Binary is `zgpl` (never `zpool`/`zfs` - must coexist with OpenZFS).

## Architecture

- `zfsgpl-ondisk` holds on-disk types and constants, each citing its spec source, with no I/O. `zfsgpl-core` layers SPA -> DMU -> DSL -> ZPL. `zfsgpl-cli` is the `zgpl` front end.

- Design: `github/project/design.md`. Roadmap: `github/project/backlog.md`.

- Rust conventions: REQUIRED reading every startup/`/clear`, before writing any Rust - `project/design.md` -> "Rust paradigm and conventions".

- Prose and general code/comment/commit style: `style-guide.md`.
