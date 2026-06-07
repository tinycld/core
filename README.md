# @tinycld/core — ⚠️ ARCHIVED

> **This repository has been merged into [`tinycld/tinycld`](https://github.com/tinycld/tinycld) and is no longer maintained. Do not use it.**

`@tinycld/core` is no longer a standalone repository. Its source — the shared
TypeScript/React runtime + UI library **and** the Go server (`server/`, module
`tinycld.org/core`) — now lives **inside the merged `tinycld` repo** at
[`tinycld/core/`](https://github.com/tinycld/tinycld/tree/main/core).

The package is unchanged from a consumer's perspective: it is still the
`@tinycld/core` workspace package and is imported through the same
`@tinycld/core/*` subpaths (`lib/*`, `ui/*`, `components/*`, `types/*`,
`file-viewer/*`, the top-level `Providers`). Only its *location* moved — from a
separate repo cloned as a workspace sibling, to a package nested inside the
`tinycld` member.

## Why

The app shell (formerly `tinycld/app`) and core were two separate repos with a
bidirectional, circular build dependency: the app imported core as its runtime
shell, while core imported the app's build-time generated output
(`@tinycld/app-generated/*`) and inherited the app's vitest/tsconfig/biome
configs by relative path. Merging them into one repo eliminates that cross-repo
coupling and the per-change coordination overhead, while preserving the
`@tinycld/core` package boundary.

## Where things are now

| Was (this archived repo) | Now (in `tinycld/tinycld`) |
| --- | --- |
| `~/code/tinycld/core/` (sibling repo) | `tinycld/core/` (nested package in the `tinycld` member) |
| `core/server/` (module `tinycld.org/core`) | `tinycld/core/server/` (same module) |
| imported as `@tinycld/core/*` | imported as `@tinycld/core/*` (unchanged) |

This repo's git history is preserved in the merged repo: core was grafted in via
`git subtree`, so `git blame` on `tinycld/core/**` resolves to these commits.

## What to do

- **Building or contributing to core:** work in
  [`tinycld/tinycld`](https://github.com/tinycld/tinycld) under `core/`.
- **Assembling a workspace:** `npx @tinycld/bootstrap@latest` now clones the
  single `tinycld` member (app shell + core) instead of separate `app` + `core`
  repos.
- **Existing clones of this repo:** discard them; they reflect the pre-merge
  layout and will not resolve against the current workspace.

For ecosystem documentation, see https://tinycld.org/docs.
