# Interactive Knowledge Graph Visualization

Interactive, browser-based visualization of the knowledge graph presented in our paper.
Everything here is **static front-end** (HTML + JavaScript + JSON + images) — no server-side
code, no database, no build step.

👉 **Live demo:** _add your GitHub Pages URL here after deploying_, e.g.
`https://<your-username>.github.io/<repo>/`

## Views

| Page | Description | Data file |
|------|-------------|-----------|
| `index.html`   | Landing page linking to all views | — |
| `full.html`    | The complete knowledge graph | `graph_export_full.json` |
| `one_node.html`| Minimal single-unit structure (relation labels drawn on edges) | `one_node.json` |
| `example1.html`| Representative subgraph #1 | `test2.json` |
| `example2.html`| Representative subgraph #2 | `test4.json` |

**Interactions:** drag the background to pan · scroll / pinch to zoom · drag a node to
reposition it (it stays pinned) · hover a node/edge to see its value or relation type ·
**Fit to Canvas** recenters the layout · **Save PNG** exports the current view.

## Viewing the graphs

These pages load their data with `fetch()`, which browsers block under the `file://`
protocol. You therefore need to open them through a **local web server** (any will do):

**Option A — VS Code Live Server**
Open this folder in VS Code, install the *Live Server* extension, right-click
`index.html` → *Open with Live Server*.

**Option B — Python (no extra packages needed)**
```bash
# from inside this folder
python -m http.server 8000
# then open http://localhost:8000/ in your browser
```

**Option C — GitHub Pages (public link)**
Push this folder to a GitHub repository and enable **Settings → Pages → Deploy from
branch**. GitHub serves it over HTTPS, so `fetch()` works and anyone with the link can
interact with the graph. This is how the live demo above is hosted.

## Local (offline) library — no CDN dependency

The force-directed graph engine
([`force-graph`](https://github.com/vasturiano/force-graph)) is **bundled locally** as
`force-graph.min.js` and referenced in each HTML file as:

```html
<script src="force-graph.min.js"></script>
```

This means the visualization works **fully offline** and does **not** depend on any
external CDN (e.g. jsDelivr/unpkg) being reachable. If you ever want to switch back to a
CDN version, replace that line with:

```html
<script src="https://cdn.jsdelivr.net/npm/force-graph"></script>
```

## Python environment (only for regenerating data)

You do **not** need Python to view the graphs. Python is only used by the helper scripts
that generate the graph JSON / figures (`networkx`, `matplotlib`, `numpy`).

Reproduce the environment with **conda** + `requirements.txt`:

```bash
conda create -n kg_visualization python=3.11 pip
conda activate kg_visualization
pip install -r requirements.txt
```

Then run the generation scripts (located in the project's `kg_visualization_kai/` folder).

## File layout

```
.
├── index.html              # landing page
├── full.html               # complete graph
├── one_node.html           # single-unit structure
├── example1.html           # subgraph 1
├── example2.html           # subgraph 2
├── force-graph.min.js      # bundled visualization library (no CDN needed)
├── graph_export_full.json  # data for full.html
├── one_node.json           # data for one_node.html
├── test2.json              # data for example1.html
├── test4.json              # data for example2.html
├── imgs/                   # node-type icons
├── fig/                    # per-ID overlay images
├── requirements.txt        # Python deps (data generation only)
└── README.md
```
