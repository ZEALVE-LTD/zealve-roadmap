# Memory bank — index

**This file is the entry point. Read it before you read any source.**
**Resolve in this order: feature → feature doc → code graph → source. Never grep the
source tree to find out where something lives; if the answer is not here, the index is
wrong and fixing the index is part of the task.**

Why: grepping finds strings, not ownership. It gives you three files that mention
`retry` and no idea which one is load-bearing, which is dead, and which one has a trap
in it that a previous engineer already paid for. This table is that knowledge, written
down once.

## Features

| Feature | Doc | Owning paths (root) | Entrypoints | Status |
| --- | --- | --- | --- | --- |
| Webhook ingest | [features/webhook-ingest.md](features/webhook-ingest.md) | `src/ingest/`, `src/models/event.py` | `POST /hooks/:provider`, `ingest_worker` | current |
| _(add yours)_ | `features/<slug>.md` | | | |

The first row is a worked example, so the shape is unambiguous. Delete it once you
have two real ones.

Status is one of: **current** (doc matches code), **stale** (code moved, doc did not —
trust the code and fix the doc), **planned** (doc describes something not built yet).
A stale row is worse than no row. If you find one, say so in your report.

## How to add a row

1. `cp features/_template.md features/<slug>.md` and fill it in. Every section has a
   one-line comment saying what belongs in it; the file is worthless half-filled.
2. Add one row here. Owning paths are directories or files the feature *owns*, not
   every file it touches — ownership means "change this and you are changing that
   feature".
3. Get the blast radius from the graph rather than from memory:
   `rk impact --base main` lists impacted files, tests and entrypoints. Paste the
   entrypoints and blast radius straight into the feature doc.
4. `rk memory update --key <KEY> --base <ref> --title <T>` appends the changelog row
   for you after a merge. It never edits **Constraints & traps** — that section is
   hand-written and must stay that way.
