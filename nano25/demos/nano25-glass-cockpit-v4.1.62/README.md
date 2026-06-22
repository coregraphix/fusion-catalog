# Avionics Glass Cockpit (v4.1.0)

Glass cockpit composition demonstrating Fusion's UI composition pipeline.
Four UI apps run side by side on a single screen :

- **PFD** — Primary Flight Display : attitude horizon, speed/altitude tapes, heading, flight director, V-speeds, FMA bar.
- **ND** — Navigation Display : compass rose, route path, waypoints, TCAS targets, weather cells, terrain map.
- **Engine** — engine gauges and unit states.
- **Alerts** — warning banners and crew alerts.

| Field | Value |
|---|---|
| Target | Nano25 (DE25-Nano, Agilex 5 SoC) |
| Fusion SDK | v4.1.52 |
| Required HW (Fusion IP) | major 4, min minor 1 |
| Binary size | 2.6 MB |
| Build mode | release / archive linkage (static lib) |
| Runtime deps | `libts`, `libm`, `glibc` (standard on Nano25 SD image) |

## Prerequisites

Before running this demo you must complete the Nano25 **one-time setup** :

1. Flash the Fusion FPGA bitstream into QSPI (see `setup-firmware-v4.1.0`).
2. Flash the Linux + Fusion SD card image (see `setup-sdcard-v4.1.0`).

Both setup steps are linked from the catalog UI.

## Run on your Nano25

The board boots a Linux system on the FPGA fabric. SSH is enabled by default
(`192.168.2.15`, user `root`).

```bash
# 1. Download glass_cockpit.elf from this catalog entry

# 2. Push it to the Nano25
scp glass_cockpit.elf root@<nano25-ip>:/root/

# 3. Run
ssh root@<nano25-ip> "chmod +x /root/glass_cockpit.elf && /root/glass_cockpit.elf"
```

The cockpit UI appears on the HDMI output connected to your Nano25.

## Stop

`Ctrl+C` in the SSH session, or :

```bash
ssh root@<nano25-ip> "pkill glass_cockpit"
```

## Build it yourself

The source is shipped inside the Fusion SDK Starter Package, under
`workspace/demos/glass_cockpit/`. Open the project in Eclipse or use the Makefile :

```bash
cd <fusion-starter>/workspace/demos/glass_cockpit
make SDK_LINK_MODE=archive FUSION_PROFILE=release
```

Output : `build/glass_cockpit`.
