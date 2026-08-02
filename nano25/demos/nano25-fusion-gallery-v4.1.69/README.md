# Fusion Gallery

An interactive tour of Fusion's capabilities, organised around the Fusion UI model
(components → layers → screens). A persistent side menu switches between views; each tile
is a small animated illustration with a live label for the animated parameter, and a
play/pause button freezes everything.

A mode toggle flips the gallery between the two composition levels of the model:

- **UI-Layer** — vector-graphics composition capabilities showcased inside a single Fusion
  graphics layer, across themed tabs: Shapes, Gradients, Patterns, Texts, and Atoms
  (scene-graph building blocks).
- **UI-Screen** — overlay composition capabilities showcased inside a Fusion display
  screen: several panels (content / image / video) layered together, each independently
  selectable and editable (move, resize, crop).

| Field | Value |
|---|---|
| Version | 4.1.63 (built against Fusion SDK v4.1.63) |
| Target | nano25 starter kit |
| Input | touchscreen, USB mouse, or both |
| Assets | image-based views load BMP files from `/root/demos/fusion_gallery/assets/` |

Note : every asset the demo needs ships with the setup — it is included in the Nano25
SD-card image, already in place under `/root/demos/fusion_gallery/assets/`. Nothing to
install.

Note : a touchscreen and a USB mouse are both strongly recommended to interact with the
demo.
