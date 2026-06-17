# fusion-catalog

**Backend repository for [fusion.coregraphix.com](https://fusion.coregraphix.com) demo distribution.**

This repo is not the customer destination. Customers evaluate Fusion
on the **Coregraphix website**, which renders the catalog from this
repo's `catalog.json` and links download buttons to this repo's
**GitHub Releases**.

```
Customer  →  fusion.coregraphix.com  →  click "Download"  →  GitHub Release URL  →  file
                       ↑
                  fetches catalog.json + READMEs
                       ↑
              this repo (cgx33/fusion-catalog)
```

If you are a **customer / evaluator**, you do not need to clone this
repo. Visit the website and follow the on-page instructions.

If you are an **internal contributor / partner / curious developer**,
read on.

---

## What this repo holds

| Path | Purpose | Consumed by |
|---|---|---|
| `catalog.json` | Master index of available setup assets + demos | Website (live fetch) |
| `nano25/setup/`, `nano25/catalog/` | Per-asset folders (README + metadata + bundle sources) | Website (READMEs fetched), team (source of truth) |
| `nano25/vendor/` | Vendor hardware documentation (Terasic) | Customers via website link |

Heavy binaries (`.jic`, `.img.gz`, `.elf`, `.zip`) are **not committed
to git**. They are distributed as **GitHub Release assets** attached
to a tag matching the asset's version. See `.gitignore` for the list.

## Repo structure

```
fusion-catalog/
├── README.md                   ← this file
├── catalog.json                ← master index (fetched by the website)
├── .gitignore                  ← excludes binary assets (live in Releases)
└── <target>/                   ← per-target content (currently: nano25/)
    ├── README.md               ← target landing (rendered on github.com)
    ├── vendor/                 ← vendor hardware documentation
    ├── setup/                  ← Tier 1: one-time provisioning
    │   ├── README.md
    │   ├── firmware/           ← Step 1: FPGA bitstream + Quartus scripts
    │   │   ├── README.md
    │   │   ├── golden_top_hps.jic                  (gitignored, Release asset)
    │   │   ├── program_qspi_flash/*.bat
    │   │   └── setup-firmware-v0.1.zip             (gitignored, Release asset)
    │   └── sdcard/             ← Step 2: Linux + Fusion image
    │       ├── README.md
    │       └── nano25-fusion.img.gz                (gitignored, Release asset)
    └── catalog/                ← Tier 2: additional ELF demos
        ├── README.md
        └── <demo>-v<x.y>/
            ├── README.md       ← rendered on the website
            ├── manifest.json
            └── <demo>.elf      (gitignored, Release asset)
```

## Customer-facing tiers (rendered on the website)

| Tier | What | Where |
|---|---|---|
| 0 | Watch a video | Website home page |
| 1 | Provision your Nano25 (FPGA + Linux SD) | `<target>/setup/` |
| 2 | Drop additional ELF demos | `<target>/catalog/` |
| 3 | Download the SDK Starter | [`fusion-sdk`](https://github.com/cgx33/fusion-sdk) releases |

Tier 0 lives on the website only.
Tier 3 lives in a separate repository.
Tiers 1 + 2 are this repo.

## How the website consumes this repo

1. The React app fetches `catalog.json` from
   `https://raw.githubusercontent.com/cgx33/fusion-catalog/main/catalog.json`
2. For each asset, it computes a download URL from the
   `release_url_template` field in catalog.json + the asset's
   `release_tag` and `filename`
3. For READMEs / instructions, it fetches the markdown via
   `https://raw.githubusercontent.com/cgx33/fusion-catalog/main/<path>`
   and renders it inline

This repo's only public-facing role is to feed those fetches. The
website is the customer destination.

## How to add or update content

### Add a new demo (Tier 2)

1. Build the demo binary from the Fusion SDK in release / archive-linkage
   mode
2. Strip the binary
3. Create `<target>/catalog/<demo>-v<x.y>/` with `README.md` and
   `manifest.json` (committed to git)
4. Add an entry to `catalog.json`'s `targets.<target>.demos[]` array
5. Commit + push these source files to git
6. Create a GitHub Release with tag `<demo>-v<x.y>` and attach the
   `.elf` as an asset

The website picks up the new demo on the next `catalog.json` fetch
(no rebuild required).

### Update Tier 1 setup

When the FPGA design changes (new bitstream) or the OS image changes:

1. Rebuild the affected asset (`.jic` for firmware, `.img.gz` for sdcard)
2. For firmware: rebuild the bundle zip
   ```powershell
   $src = "nano25\setup\firmware"
   Compress-Archive -Path "$src\golden_top_hps.jic","$src\program_qspi_flash","$src\README.md" -DestinationPath "$src\setup-firmware-vX.Y.zip"
   ```
3. Bump the corresponding `release_tag` in `catalog.json`
4. Commit + push the catalog change
5. Create a new GitHub Release with the new tag and asset

If both firmware and sdcard need a coordinated update (incompatible
versions), do them in lockstep so customers always pair matching
versions.

## Internal documentation

The strategy, build pipeline, and web-designer brief live in the
private `fusion-sdk` repository under `fusion-sdk/demo/`. They are
not part of this public repository:

- `FUSION_DEMO_STRATEGY.md` — internal strategy, hosting decisions, roadmap
- `FUSION_DEMO_WEBDESIGN.md` — self-contained brief for the web-designer

## Cross-references

- Fusion SDK source + packaged releases : [`fusion-sdk`](https://github.com/cgx33/fusion-sdk) (private)
- Coregraphix website : [`fusion.coregraphix.com`](https://fusion.coregraphix.com)
