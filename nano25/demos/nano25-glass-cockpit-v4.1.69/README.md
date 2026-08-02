# Avionics Glass Cockpit

A full glass cockpit built with the Fusion UI model: four UI apps composed as separate
layers on a single display screen.

- **PFD** — Primary Flight Display (attitude, speed/altitude, heading, flight director).
- **ND** — Navigation Display (compass, route, traffic, weather over a terrain map).
- **Engine** — engine and systems gauges.
- **Alerts** — crew alerts and warning banners.

| Field | Value |
|---|---|
| Version | 4.1.63 (built against Fusion SDK v4.1.63) |
| Target | nano25 starter kit (DE25-Nano, Agilex 5 SoC) |
| Input | touchscreen and/or USB mouse, optional (RTUI home button + diagnostics dashboard) — the cockpit itself runs unattended |
| Assets | the ND terrain map and PFD synthetic-vision video load from `/root/demos/glass_cockpit/` |

Note : every asset the demo needs ships with the setup — it is included in the Nano25
SD-card image, already in place under `/root/demos/glass_cockpit/`. Nothing to install.

Note : a touchscreen and a USB mouse are both strongly recommended to interact with the
demo.
