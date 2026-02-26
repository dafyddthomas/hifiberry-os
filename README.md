# HiFiBerry OS (Next Generation)

HiFiBerry OS is a Debian package-based audio platform for Raspberry Pi with HiFiBerry HATs.
This repository contains installer scripts, packaging for core services, and player packages.

## Highlights

- PipeWire-based audio stack
- AudioControl-backed WebUI and player orchestration
- Package-driven installation (`hbos-minimal`, `hbos-full`, `hbos-test`)
- Per-user `systemd` services for players

## Supported Platform

- Raspberry Pi 3/4/5 (64-bit)
- Debian 13 (Trixie) target
- Debian 12 (Bookworm) can be upgraded using `upgrade-to-trixie`

## Quick Install

### Option A: Clone and run the installer (recommended)

```bash
git clone https://github.com/hifiberry/hifiberry-os.git
cd hifiberry-os
./install-all
```

`install-all`:
- validates Debian version
- adds the HiFiBerry APT repository
- installs `hbos-minimal`
- configures user/session defaults for player services

### Option B: Add repository only

```bash
./addrepo
```

Then install packages manually, for example:

```bash
sudo apt update
sudo apt install -y hbos-minimal
```

## Package Variants

- `hbos-minimal`: core HiFiBerry OS components (PipeWire + MPD + AudioControl + WebUI)
- `hbos-full`: minimal plus major streaming players (Librespot, Shairport, Squeezelite, RAAT)
- `hbos-test`: diagnostics-oriented profile with test tooling

For detailed meta-package information, see `packages/hifiberryos/README.md`.

## Upgrade Path (Bookworm -> Trixie)

If you are on Debian 12 (Bookworm), run:

```bash
./upgrade-to-trixie
```

After the upgrade completes and you reboot, run `./install-all`.

## Development: Building Packages

This repository uses Debian packaging with `sbuild`.

### Build one package

```bash
cd packages/<package-name>
./build.sh
```

### Build all packages

```bash
cd packages
./build-all
```

Force clean rebuild:

```bash
cd packages
./build-all --clean
```

For full build environment guidance, see `packages/build.md`.

## Repository Layout

- `install-all`, `addrepo`, `upgrade-to-trixie`: host install/upgrade scripts
- `packages/`: package sources, Debian metadata, package build/clean scripts
- `scripts/`: helper scripts for chroots and cross-compile `sbuild` workflows

## Accessing the UI

The WebUI is available at:

```text
http://<device-ip>/
```
