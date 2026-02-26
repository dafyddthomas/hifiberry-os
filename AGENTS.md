# AGENTS.md

Guidance for coding agents working in this repository.

## Scope

These instructions apply to the whole repository rooted at this directory.

## Project Overview

- This repo packages HiFiBerry OS components as Debian packages.
- Most work happens under `packages/<name>/` with package-specific `build.sh` and `clean.sh`.
- Runtime target is Debian 13 (Trixie) on Raspberry Pi (arm64).

## Key Paths

- `README.md`: user-facing installation and workflow documentation
- `install-all`, `addrepo`, `upgrade-to-trixie`: install/upgrade scripts
- `packages/build-all`: build every package directory that has `build.sh`
- `packages/build.md`: build environment notes and troubleshooting
- `scripts/`: helper tooling (`create-chroot`, `enable-cross-compile`, etc.)

## Recommended Workflow

1. Read the target package directory before editing.
2. Keep changes minimal and scoped to the requested task.
3. If package metadata changes, verify version/changelog consistency.
4. Run the smallest relevant verification command(s) before finishing.

## Build and Verification

Build a package:

```bash
cd packages/<package-name>
./build.sh
```

Clean + rebuild a package:

```bash
cd packages/<package-name>
./clean.sh
./build.sh
```

Build all packages:

```bash
cd packages
./build-all
```

Clean build all:

```bash
cd packages
./build-all --clean
```

## Packaging Conventions

- Prefer editing Debian packaging files in `packages/*/src/debian/` when changing package behavior.
- Many build scripts derive version information from `debian/changelog`; keep it accurate.
- Do not assume cross-compile is active unless `scripts/sbuild` wrapper is present.

## Documentation Rules

- Keep top-level docs aligned with current scripts and package names.
- Use explicit Debian version references when relevant (Bookworm vs Trixie).
- Avoid stale references to removed packages/services.

## Safety Notes

- Do not use destructive git commands unless explicitly requested.
- Treat uncommitted user changes as intentional; do not revert unrelated files.
