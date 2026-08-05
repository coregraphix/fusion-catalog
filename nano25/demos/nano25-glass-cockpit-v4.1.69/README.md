# Avionics Glass Cockpit

A full glass cockpit built with the Fusion UI model: four UI apps composed as separate
layers on a single display screen.

- **PFD** — Primary Flight Display (attitude, speed/altitude, heading, flight director).
- **ND** — Navigation Display (compass, route, traffic, weather over a terrain map).
- **Engine** — engine and systems gauges.
- **Alerts** — crew alerts and warning banners.

| Field | Value |
|---|---|
| Version | 4.1.69 (built against Fusion SDK v4.1.69) |
| Target | nano25 starter kit (DE25-Nano, Agilex 5 SoC) |
| Input | touchscreen and/or USB mouse — optional, the demo plays a scripted scenario on its own |
| Assets | the ND terrain map and PFD synthetic-vision video load from `/root/demos/glass_cockpit/` |

Note: every asset the demo needs ships with the setup — it is included in the Nano25
SD-card image, already in place under `/root/demos/glass_cockpit/`. Nothing to install.

Note: the whole cockpit is interactive, not just the scenario — every panel responds to
touch/mouse. Input is optional (the scenario runs unattended), but a touchscreen or USB
mouse is recommended to explore the interactive side.
