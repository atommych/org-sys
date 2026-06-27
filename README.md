# org-sys

This repository contains a single-page visual experiment rendered with the HTML5 Canvas API.

## Repository structure

- `/home/runner/work/org-sys/org-sys/index.html` — complete app (HTML, CSS, and JavaScript in one file).
- `/home/runner/work/org-sys/org-sys/README.md` — project documentation.

## What the HTML file does

`index.html` renders an animated network of isometric “cubes” connected by edges:

- 13 nodes are defined in `items` (symbol + color palette) and `positions` (initial layout).
- Connections are defined in `edges`.
- Nodes float slightly using sinusoidal animation (`phase` and `speed` per node).
- Pulse particles are spawned and move along random edges to simulate network activity.
- Each node is draggable with mouse and touch events.

## Technical analysis of `index.html`

### 1) Layout and styling
- Dark full-page background.
- A centered `<canvas>` (`680x720`) used for all rendering.
- Cursor feedback (`grab` / `grabbing`) while interacting.

### 2) Data model
- `items`: visual identity of each cube (symbol, light color, dark color).
- `positions`: initial coordinates.
- `edges`: graph topology (which nodes are connected).
- `nodes`: runtime state (position, animation phase/speed, drag state).
- `pulses`: transient objects moving on edges.

### 3) Interaction
- `hitTest()` detects whether the pointer is over a node.
- Drag flow: `startDrag()` → `moveDrag()` → `endDrag()`.
- Movement is clamped to canvas bounds.
- Works for both desktop (`mouse*`) and mobile (`touch*`) events.

### 4) Rendering pipeline
- `frame(ts)` runs through `requestAnimationFrame`.
- Clears canvas, updates pulses, draws dashed edges, draws pulse dots, then draws cubes.
- `drawCube()` paints pseudo-3D faces and overlays each node’s symbol.

### 5) Utility behavior
- `hexRgb()` converts hex colors for rgba usage.
- `getPos()` maps pointer/touch coordinates to canvas coordinates with scaling.

## How to run

Open `/home/runner/work/org-sys/org-sys/index.html` in a browser.

No build step or external dependency is required.