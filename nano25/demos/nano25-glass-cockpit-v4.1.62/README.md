# Avionics Glass Cockpit

Glass cockpit composition demonstrating Fusion's UI composition pipeline.
Four UI apps run side by side on a single screen :

- **PFD** — Primary Flight Display : attitude horizon, speed/altitude tapes, heading, flight director, V-speeds, FMA bar.
- **ND** — Navigation Display : compass rose, route path, waypoints, TCAS targets, weather cells, terrain map.
- **Engine** — engine gauges and unit states.
- **Alerts** — warning banners and crew alerts.

| Field | Value |
|---|---|
| Target | Nano25 (DE25-Nano, Agilex 5 SoC) |
| Fusion SDK | v4.1.62 |
| Required HW (Fusion IP) | major 4, min minor 1 |
| Build mode | release / archive linkage (static lib) |
| Runtime deps | `libts`, `libm`, `glibc` (standard on Nano25 SD image) |

## Run

Requires the one-time Nano25 setup (FPGA bitstream + SD card image),
linked from the catalog UI.

Deploy and launch `glass_cockpit.elf` following the generic procedure
in [HOW_TO_RUN.md](../HOW_TO_RUN.md). The cockpit UI appears on the
HDMI output.

## Build it yourself

The source is shipped inside the Fusion SDK Starter Package, under
`workspace/demos/glass_cockpit/`. Open the project in Eclipse or use the Makefile :

```bash
cd <fusion-starter>/workspace/demos/glass_cockpit
make SDK_LINK_MODE=archive FUSION_PROFILE=release
```

Output : `build/glass_cockpit`.
