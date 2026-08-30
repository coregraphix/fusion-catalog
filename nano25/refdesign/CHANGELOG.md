# Changelog — nano25 reference design

Notable changes to the nano25 reference design, newest first.

## [Unreleased]

## [4.2.8] - 2026-08-29

### Changed

- Quartus project migrated to Quartus Prime Pro 26.1.
- Fusion IP updated to v4.2.3 (data32 display bus, reduced I/O pixel
  formats — see `q26.1/ip/cgx_fusion/docs/CHANGELOG.md`).
- EMIF LPDDR4 calibration driver moved inside the Platform Designer system
  (previously instantiated in the board top-level); board top-level trimmed
  accordingly.

### Removed

- Stale unreferenced `.ip` files left over from the initial bring-up.
