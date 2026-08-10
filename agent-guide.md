# yfiles-jupyter-graphs Agent Guide

Reference for coding agents working with `yfiles-jupyter-graphs` (v2.x).

## Install

```bash
pip install yfiles-jupyter-graphs
```

**Note for Google Colab:** To render the widget correctly, you need to enable the custom widget manager:
```python
try:
  import google.colab
  from google.colab import output
  output.enable_custom_widget_manager()
except:
  pass
```

## Core import pattern

```python
from yfiles_jupyter_graphs import GraphWidget, Node, Edge, Layout
from yfiles_jupyter_graphs import NodeStyle, NodeShape, EdgeStyle, DashStyle
from yfiles_jupyter_graphs import LabelStyle, LabelPosition, FontWeight, TextWrapping, TextAlignment
```

## Minimal working example

```python
from yfiles_jupyter_graphs import GraphWidget, Node, Edge

w = GraphWidget(
    nodes=[
        Node(id=0, properties={"label": "A"}),
        Node(id=1, properties={"label": "B"}),
    ],
    edges=[
        Edge(start=0, end=1, properties={"label": "connects"}),
    ],
    directed=True,
)
display(w)
```

## GraphWidget constructor kwargs

| Kwarg                | Type               | Notes                                                                                                                                  |
|----------------------|--------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `nodes`              | `List[Node\|dict]` | Each node needs `id`. Additional properties can be added in optional `properties` dict.                                                |
| `edges`              | `List[Edge\|dict]` | Each edge needs `start` and `end` matching node `id`s. Additional properties can be added in optional `properties` dict.               |
| `directed`           | `bool`             | Whether edge direction is visualized. Per-edge override via `directed_mapping` or `edge_styles_mapping`.                               |
| `graph`              | object             | Alternative to `nodes`/`edges` to import graphs directly from `networkx`, `graph_tool`, `neo4j`, `igraph`, `pygraphviz`, and `pandas`. |
| `graph_layout`       | `Layout\|str`      | Default: force-directed (`"organic"`).                                                                                                 |
| `license`            | dict               | Domain-specific license key, unnecessary for pre-approved domans (see below).                                                          |
| `context_start_with` | str                | Open sidebar panel at start: `"About"`, `"Search"`, `"Data"`, `"Neighborhood"`.                                                        |
| `overview_enabled`   | bool               | Whether overview panel is expanded.                                                                                                    |
| Any mapping prop     |                    | All `*_mapping` properties can also be passed here.                                                                                    |

## Data classes

### Node
```python
Node(id=0, properties={"label": "Name", "group": "A"})
```
- `id`: `str | int` — must be unique
- `properties`: `dict[str, Any]` — optional 

### Edge
```python
Edge(start=0, end=1, properties={"label": "knows"})
```
- `start`, `end` — referencing node `id`s
- `id`: `str | int` — optional, auto-generated UUID if omitted
- `properties`: `dict[str, Any]` — optional

## Importing from other graph libraries

```python
# Pass graph object directly to constructor or use import_graph()
w = GraphWidget(graph=nx_graph)        # networkx
w = GraphWidget(graph=ig_graph)        # igraph
w = GraphWidget(graph=session.run(cypher).graph())  # neo4j
w.import_graph(pandas_dataframe)       # pandas (rows = edges; needs "source", "target" columns)
w.import_graph(pygraphviz_graph)       # pygraphviz
```

**Pandas import rules:** each row is an edge; columns `source` and `target` define the connection; a `label` column auto-labels edges; additional columns go into `properties`.

**NetworkX import rules:** node identifiers are saved under property key `label` (or `yf_label` if `label` already exists). Subgraphs (graph-as-node) are not supported.

**Neo4j import rules:** node labels joined with `:` become the `label` property; relationship properties available via `properties`. Default label priority: `name > title > label > description > caption > text`.

## Layouts

Set via `w.graph_layout = Layout.HIERARCHICAL` or the convenience method `w.hierarchical_layout()`.

| Layout enum                     | String value               | Use case                                                                    |
|---------------------------------|----------------------------|-----------------------------------------------------------------------------|
| `Layout.CIRCULAR`               | `"circular"`               | Ring with bundled edges                                                     |
| `Layout.CIRCULAR_STRAIGHT_LINE` | `"circular_straight_line"` | Ring with straight edges                                                    |
| `Layout.HIERARCHICAL`           | `"hierarchical"`           | Layered DAGs, flow diagrams                                                 |
| `Layout.ORGANIC`                | `"organic"`                | Force-directed, general purpose (default)                                   |
| `Layout.INTERACTIVE_ORGANIC`    | `"interactive_organic"`    | Force-directed with live user interaction                                   |
| `Layout.ORTHOGONAL`             | `"orthogonal"`             | Grid/structured diagrams                                                    |
| `Layout.RADIAL`                 | `"radial"`                 | Central node with rings                                                     |
| `Layout.TREE`                   | `"tree"`                   | Branching tree from root                                                    |
| `Layout.MAP`                    | `"map"`                    | Geo-coordinates on world map, uses positions form `node_coordinate_mapping` |
| `Layout.ORTHOGONAL_EDGE_ROUTER` | `"orthogonal_edge_router"` | Reroutes edges only, no node movement                                       |
| `Layout.ORGANIC_EDGE_ROUTER`    | `"organic_edge_router"`    | Smooth curved edge routing                                                  |
| `Layout.NO_LAYOUT`              | `"no_layout"`              | Use positions from `node_position_mapping`                                  |

## Data-driven mapping properties

All mappings accept either a **property key string** (resolved from `item["properties"]`) or a **callable** `lambda item: ...` or `lambda index, item: ...`.
Set to `None` to remove a mapping.

### Label
```python
w.node_label_mapping = "label"                          # default, uses properties["label"]
w.node_label_mapping = lambda n: n["properties"]["name"]
w.edge_label_mapping = lambda e: LabelStyle(text=e["properties"]["type"], color="#FF0000")
```

### Color
```python
w.node_color_mapping = lambda n: "#FF0000" if n["properties"]["active"] else "#AAAAAA"
w.edge_color_mapping = "color"  # use properties["color"]
```

### Node style
```python
w.node_styles_mapping = lambda n: NodeStyle(
    color="#4A90D9",
    shape=NodeShape.ROUND_RECTANGLE,
    image="https://example.com/icon.png",  # or data URL, alternative to `shape` and `color`
)
```
`NodeShape` values: `ELLIPSE`, `HEXAGON`, `HEXAGON_STANDING`, `OCTAGON`, `PILL`, `RECTANGLE`, `ROUND_RECTANGLE`, `TRIANGLE`, `SQUIRCLE`

### Edge style
```python
w.edge_styles_mapping = lambda e: EdgeStyle(
    color="#333333",
    directed=True,
    thickness=2.0,
    dash_style=DashStyle.DASH,  # or custom string "5 10"
)
w.directed_mapping = lambda e: e["properties"].get("directed", False)
w.edge_thickness_factor_mapping = lambda e: e["properties"]["weight"]
```
`DashStyle` values: `SOLID`, `DASH`, `DOT`, `DASH_DOT`, `DASH_DOT_DOT`

### Geometry
```python
w.node_scale_factor_mapping = lambda n: n["properties"]["size"]     # multiplied to base size
w.node_size_mapping = lambda n: (100, 50)                           # (width, height)
w.node_position_mapping = lambda n: (n["properties"]["x"], n["properties"]["y"])
w.node_layout_mapping = lambda n: (x, y, width, height)            # full bounding box
```
Position mappings are overwritten by automatic layouts unless `Layout.NO_LAYOUT` is used.

### Geospatial (map layout)
```python
w.node_coordinate_mapping = lambda n: (n["properties"]["lat"], n["properties"]["lon"])
w.graph_layout = Layout.MAP
```

### Grouping / nesting
```python
# Group nodes using an existing parent node id from the dataset
w.node_parent_mapping = lambda n: n["properties"]["parent_id"]

# Create new group nodes dynamically (not in dataset)
w.node_parent_group_mapping = "country"                             # string key shorthand
w.node_parent_group_mapping = lambda n: {
    "label": n["properties"]["country"],
    "color": "#9F4499",
}
```
Note: Dynamically created group nodes from `node_parent_group_mapping` are also passed to other node mappings (like `node_label_mapping`). Ensure these mappings safely handle missing properties (e.g., using `n['properties'].get('key')`) to avoid `KeyError`.

### Heatmap
```python
w.heat_mapping = lambda n: n["properties"]["score"]  # must be normalized 0.0–1.0
```

### Layout fine-tuning
```python
w.node_type_mapping = lambda n: n["properties"]["category"]        # adjacent placement of same type
w.node_cell_mapping = lambda n: (n["properties"]["row"], n["properties"]["col"])  # hierarchical grid hint
```

### Property remapping
```python
w.node_property_mapping = lambda n: {"label": n["properties"]["name"]}
```

## LabelStyle reference

```python
LabelStyle(
    text="Hello",
    font="Arial",
    font_size=14,
    font_weight=FontWeight.BOLD,
    color="#000000",
    background_color="#FFFF00",
    position=LabelPosition.SOUTH,
    maximum_width=120,
    maximum_height=40,
    wrapping=TextWrapping.WRAP_WORD_ELLIPSIS,
    text_alignment=TextAlignment.CENTER,
)
```

`LabelPosition`: `CENTER`, `NORTH`, `EAST`, `SOUTH`, `WEST`  
`FontWeight`: `BOLD`, `BOLDER`, `NORMAL`, `LIGHTER`  
`TextWrapping`: `NONE`, `CLIP`, `TRIM_CHARACTER`, `TRIM_CHARACTER_ELLIPSIS`, `TRIM_WORD`, `TRIM_WORD_ELLIPSIS`, `WRAP_CHARACTER`, `WRAP_CHARACTER_ELLIPSIS`, `WRAP_WORD`, `WRAP_WORD_ELLIPSIS`  
`TextAlignment`: `CENTER`, `LEFT`, `RIGHT`

## UI controls

```python
w.sidebar = {"enabled": True, "start_with": "Search"}  # or just True/False
w.overview = True
w.neighborhood = {"max_distance": 2, "selected_nodes": [0]}  # or just an int
nodes, edges = w.selection  # read currently selected items
```

## License (non-standard domains)

```python
GraphWidget.license = {          # set once, applies globally
    "id": "...",
    "domains": ["my.domain.com"],
    "expiry": "2024-01-05",
    "version": "1.0",
    "signature": "..."
}
```

Pre-approved domains (no license needed): JupyterLab, VS Code, Google Colab, Amazon SageMaker, Azure ML Studio, Kaggle, `localhost`, `127.0.0.1`.

## Gotchas

- `Node.id` must be unique across all nodes.
- `Edge.start` / `Edge.end` must reference existing node `id`s.
- Automatic layouts overwrite `node_position_mapping` — use `Layout.NO_LAYOUT` to preserve positions.
- `heat_mapping` values must be normalized to `[0.0, 1.0]`.
- `node_parent_mapping` only works when parent nodes exist in the dataset; use `node_parent_group_mapping` to create group nodes on the fly.
- Dynamically created group nodes are also passed to other mappings (like `node_label_mapping`). Ensure these mappings safely handle missing properties.
- The legacy `set_*` / `get_*` / `del_*` methods are deprecated — assign properties directly.
- For richer Neo4j/Kuzu/SPARQL workflows, prefer the dedicated packages (yfiles_jupyter_graphs_for_neo4j, yfiles_jupyter_graphs_for_kuzu, yfiles_jupyter_graphs_for_sparql) over the built-in importer.
