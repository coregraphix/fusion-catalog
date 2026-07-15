# Fusion Gallery

Interactive tour of Fusion capabilities. A persistent side menu switches between themed
tabs; every tile is a small, focused, animated illustration of one feature, with a live
label showing the parameter being animated. A play/pause button freezes all animations.

Current tabs :

- **Shapes** — vector paths and strokes : basic shapes, arcs (types and sweep), Bezier
  curves, fill rules, line caps, line joins, dash patterns, paint combinations.
- **Gradients** — linear, radial and conic gradients : color ramps, spread modes,
  transforms, animated stops.
- **Patterns** — bitmap paints sampled from real images : spread modes (pad, repeat,
  reflect), zoom, rotation, scrolling, per-pixel transparency.
- **Bounce** — scene-graph atoms animated by the reference-scene clock.

More tabs are in development (text, masks, display layers).

| Field | Value |
|---|---|
| Status | preview — under active development |
| Version | 4.1.0 (build 0 : not an official release build) |
| Target | nano25 starter kit |
| Input | touchscreen, USB mouse, or both |
| Assets | the Patterns tab loads BMP images from `/root/demos/fusion_gallery/assets/` |

Note : this preview build expects its image assets on the target. Without them the
Patterns tab shows empty tiles; all other tabs are self-contained.
