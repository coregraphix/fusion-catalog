# Changelog — Fusion SDK

Notable changes to the Fusion SDK, newest first. Record every notable change
under `[Unreleased]` as you make it; `sdk.build` stamps this section with the
release version and injects the history into the shipped release notes.

## [4.2.70] - 2026-08-29

### Changed

- Embedded Fusion IP updated to v4.2: data32 external video buses, reduced
  I/O pixel formats, integrator manual (`FUSION_IP.md`) and changelog shipped
  inside the IP package — see `ip/cgx_fusion/docs/CHANGELOG.md`.
- The SDK now requires Fusion IP hardware v4.2 (runtime check:
  major = 4, minor >= 2).
