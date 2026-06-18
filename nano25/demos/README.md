# Nano25 Demo Catalog (Tier 1 — ELF binaries)

Pre-built Fusion demos for the Nano25 evaluation board. Each demo is a
self-contained ELF binary (statically linked against `libfusion.a` and
`libatk.a`) that runs on a stock Nano25 Linux image.

## Audience

Developers who already have a working Nano25 with SSH access. Drop the
ELF on the board, run it, see Fusion in action — no SDK download, no
toolchain setup, no compilation. **5-minute evaluation**.

For a zero-setup experience (no SSH needed), see
`../image-sdcard/` (Tier 2 — bootable SD image).

For full development capability, download the Fusion SDK Starter
(Tier 3 — see `https://github.com/cgx33/fusion-sdk`).

## Available demos

| Demo | Description | Version |
|---|---|---|
| [cockpit-pfd-v0.1](cockpit-pfd-v0.1/) | Avionics Primary Flight Display | 0.1 |
| [cockpit-eicas-v0.1](cockpit-eicas-v0.1/) | Engine Indication & Crew Alerting System | 0.1 |
| [cockpit-multi-v0.1](cockpit-multi-v0.1/) | Integrated Glass Cockpit (PFD + EICAS + Alerts) | 0.1 |

For machine-readable metadata, see
[`../catalog.json`](../../catalog.json) at the repo root — the
website React frontend consumes this to render the demos page.

## Quick start (any demo)

```bash
# 1. Download the demo's ELF (e.g. cockpit-pfd.elf)
# 2. Deploy:
scp cockpit-pfd.elf root@<nano25-ip>:/root/
# 3. Run:
ssh root@<nano25-ip> "chmod +x /root/cockpit-pfd.elf && /root/cockpit-pfd.elf"
```

Each demo's individual README documents its specific deploy/run flow
and runtime dependencies.

## Per-demo structure

```
cockpit-<name>-v<version>/
├── README.md           ← end-user documentation (run/stop/troubleshoot)
├── manifest.json       ← machine-readable metadata (consumed by website)
└── <name>.elf          ← stripped, archive-linked, release ELF
```
