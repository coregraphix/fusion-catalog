# Changelog — nano25 reference design

Notable changes to the nano25 reference design, newest first. Each entry reads
`ID · area · subject` : the ID is unique across releases and never reused, so that a change can be
referred to by its ID.

----------------------------------------------------------------------------------------------------

## [4.3.9] - 2026-10-14

### Changed

- **NANO25-0006 · IP · Fusion IP v4.3.13** — Fusion IP updated to v4.3.13 : up to eight video
  inputs, optional memory port for the video captures — see
  `q26.1/ip/cgx_fusion/docs/CHANGELOG.md`.
- **NANO25-0005 · Timing · GPU clock** — GPU clock Fmax increased from 250 MHz to 320 MHz.

----------------------------------------------------------------------------------------------------

## [4.2.8] - 2026-08-29

### Changed

- **NANO25-0004 · Quartus · Quartus 26.1** — Quartus project migrated to Quartus Prime Pro 26.1.
- **NANO25-0003 · IP · Fusion IP v4.2.3** — Fusion IP updated to v4.2.3 : data32 display bus,
  reduced I/O pixel formats — see `q26.1/ip/cgx_fusion/docs/CHANGELOG.md`.
- **NANO25-0002 · System · EMIF calibration** — EMIF LPDDR4 calibration driver moved inside the
  Platform Designer system (previously instantiated in the board top-level) ; board top-level
  trimmed accordingly.

### Removed

- **NANO25-0001 · System · Stale IP files** — stale unreferenced `.ip` files left over from the
  initial bring-up.
