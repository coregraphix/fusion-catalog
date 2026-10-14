# Changelog — Fusion SDK

Notable changes to the Fusion SDK, newest first. Each entry reads `ID · area · subject` : the ID
is unique across releases and never reused, so that a change can be referred to by its ID.

----------------------------------------------------------------------------------------------------

## [4.3.72] - 2026-10-14

### Changed

- **SDK-0013 · IP · Embedded Fusion IP** — updated to v4.3.13 — see
  `ip/cgx_fusion/docs/CHANGELOG.md`.

----------------------------------------------------------------------------------------------------

## [4.3.71] - 2026-09-29

### Added

- **SDK-0012 · Fusion · Stop** — `cgx_fusion_stop(dev, timeout_ms)` stops Fusion before the
  application exits, so that the next one starts on a quiet device.
- **SDK-0011 · Memory · Video port** — supports the dedicated video capture port of Fusion IP 4.3,
  typically to partition graphics rendering and video captures, and improve determinism and
  performance.
- **SDK-0010 · DMA · Wait timeout** — `cgx_dma_wait()` reports a transfer still pending after
  2 s as `CGX_ERROR_TIMEOUT` instead of waiting forever.

### Changed

- **SDK-0009 · IP · Embedded Fusion IP** — updated to v4.3.11 : up to eight video inputs, optional
  memory port for the video captures — see `ip/cgx_fusion/docs/CHANGELOG.md`.
- **SDK-0008 · IP · Hardware requirement** — the SDK requires Fusion IP v4.3 (major = 4,
  minor >= 3) ; a v4.2 IP is refused at creation.
- **SDK-0007 · Fusion · Memory pools** — `cgx_fusion_create()` takes a
  `cgx_fusion_memory_t` : the default pool of each memory port, and the pool of each video
  Surface, so that video Surfaces can be dispatched across two memory banks.
- **SDK-0006 · Fusion · Warm start** — `cgx_fusion_create()` stops Fusion before bringing it
  up : an application that ended without stopping it no longer blocks the next one.
- **SDK-0005 · Memory · Port API** — the memory-phy API refactored into the memory-port API
  (`cgx_memory_port_*`).
- **SDK-0004 · Targets · nano25 launcher** — the launcher stops Fusion when the application
  exits, and sends the SDK traces to syslog as well.

### Fixed

- **SDK-0003 · Graphics · VGR status** — the NULL-handle error `VGR_STS_ERROR` no longer
  collides with a hardware status bit.

----------------------------------------------------------------------------------------------------

## [4.2.70] - 2026-08-29

### Changed

- **SDK-0002 · IP · Embedded Fusion IP** — updated to v4.2 : data32 external video buses,
  reduced I/O pixel formats, integrator manual (`FUSION_IP.md`) and changelog shipped inside the
  IP package — see `ip/cgx_fusion/docs/CHANGELOG.md`.
- **SDK-0001 · IP · Hardware requirement** — the SDK now requires Fusion IP hardware v4.2
  (runtime check: major = 4, minor >= 2).
