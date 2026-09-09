# Maintenance

## Background

Maintained fork: `0xble/Peekaboo` of `openclaw/Peekaboo`; maintained and
upstream branch `main`. This temporary isolated checkout is remote-only, not a
runtime canonical checkout. Accepted baseline:
`98b080a92bbf6dc1c4c7c6addc8acf36045b6499`. Publish only to `origin`; never
push upstream.

## Preserve

- Fork version suffix and portable CLI upgrade wiring survive upstream refreshes.
- Source synchronization, publication, installation, and runtime activation are
separate stages with separate authorization and proof.

## Active patches

### PEEKABOO-001: `fix(fork): make peekaboo upgrade path portable`

- **Status:** Active; `a043df58`, `7baca220`.
- **Behavior:** fork upgrade script installs the CLI from a portable path.
- **Surfaces:** `bin/upgrade`, `package.json`.
- **Upstream issue:** None after checked 2026-09-09.
- **Upstream PR:** None after checked 2026-09-09.
- **Regression:** `bash -n bin/upgrade bin/smoke`; `pnpm run test:safe` passes without an install.
- **Rollback:** revert both commits and remove only the fork upgrade wiring.
- **Retire when:** an authorized disposition retires this source path or an adopted upstream equivalent passes proof.

### PEEKABOO-002: `fix(fork): restore peekaboo version suffix after sync`

- **Status:** Active; `3106de0d` after baseline-sync `8c94c5b8`.
- **Behavior:** fork build metadata keeps the `0xble` suffix after reconciliation.
- **Surfaces:** CLI/Mac/inspector/playground project metadata, `version.json`, `LOCAL.md`.
- **Upstream issue:** None after checked 2026-09-09.
- **Upstream PR:** None after checked 2026-09-09.
- **Regression:** `pnpm run lint`, `pnpm run format`, and `pnpm run build:cli` pass.
- **Rollback:** revert `3106de0d`; retain the sync commit only if its upstream ancestry remains needed.
- **Retire when:** an approved unbranded distribution or verified upstream equivalent replaces it.

## Update

Every maintenance run fetches `origin` and latest `upstream/main`, reconciles
`main`, preserves only these active records, and runs the declared regression,
test, and build proof before authorized publication. Immediately before `Updated`
or `Already current`, fetch upstream again and prove no upstream-only commits;
otherwise report `Blocked` with stage, refs, and evidence. Update this contract
with each patch addition, change, or retirement; missing coverage blocks
publication.

## Verify

```text
bash -n bin/upgrade bin/smoke
pnpm run lint
pnpm run format
pnpm run test:safe
pnpm run build:cli
git rev-list --left-right --count upstream/main...main
```

Require a fresh final fetch with zero upstream-only commits and local/`origin`
SHA parity after authorized publication. Installation and runtime proof are only
required in separately authorized stages.