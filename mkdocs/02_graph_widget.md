# `GraphWidget` API documentation
The main class of the widget that can be imported from the `yfiles_jupyter_graphs` module.

## Constructor

| Argument             | Type                | Description                                                                                                                                                                  | Default |
|----------------------|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| `widget_layout`      | `ipywidgets.Layout` | Optional. Specifies the widget's size.<br> See [ipywidgets.Layout](https://ipywidgets.readthedocs.io/en/7.6.3/examples/Widget%20Styling.html#The-layout-attribute) for more. | `None`  |
| `overview_enabled`   | `bool`              | Optional. Whether the overview is expanded.<br>By default, dependant on the widget's width.                                                                                  | `None`  |
| `context_start_with` | `str`               | Optional. The sidebar panel that should<br> be opened at start. Collapsed by default.<br> Supported values:<br>`"About"`, `"Search"`, `"Data"`, `"Neighborhood"`.            | `None`  |
| `graph`              | `object`            | Optional. Specify a graph object to import<br> from start.                                                                                                                   | `None`  |

The widget's data and configuration properties can also be provided as constructor keyword
arguments. This includes `nodes`, `edges`, `license`, and the data-driven visualization
mapping properties described below, such as `node_label_mapping`, `node_color_mapping`,
`node_layout_mapping`, `edge_label_mapping`, and `directed_mapping`. Passing a property as a
constructor keyword argument is equivalent to assigning it after construction, for example:

```python
w = GraphWidget(nodes=nodes, edges=edges, node_label_mapping="label")
```

### Example

```Python
from yfiles_jupyter_graphs import GraphWidget, Node, Edge
w = GraphWidget()
w.nodes = [
    Node(id=0, properties={"firstName": "Alpha", "label": "Person A"}),
    Node(id=1, properties={"firstName": "Bravo", "label": "Person B"}),
    Node(id=2, properties={"firstName": "Charlie", "label": "Person C", "has_hat": False}),
    Node(id=3, properties={"firstName": "Delta", "label": "Person D", "likes_pizza": True})
]
w.edges = [
    Edge(start=0, end=1, properties={"since": "1992", "label": "knows"}),
    Edge(start=1, end=3, properties={"label": "knows", "since": "1992"}),
    Edge(start=2, end=3, properties={"label": "knows", "since": "1992"}),
    Edge(start=0, end=2, properties={"label": "knows", "since": 234})
]
display(w)
```

See the [example notebooks](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/00_toc.ipynb) for more.

## Providing data

To pass data to the widget, you need to set the `nodes` and `edges` properties of the widget. There are only few requirements to the structuring of the provided data:

* `nodes: List[Union[Node, dict[str, Any]]]`
    * Each node must provide an `id` property.

* `edges: List[Union[Edge, dict[str, Any]]]`
    * Each edge must provide a `start` and `end` property that resolve to the node `id`s to form the graph structure.

Optionally, provide additional properties in a `properties` property.

Instead of plain dictionaries, the [`Node`](#node) and [`Edge`](#edge) dataclasses can be used, which are the
preferred way due to better developer experience (e.g., code-completion). Plain dictionaries are still
supported for backwards compatibility.

```python
from yfiles_jupyter_graphs import GraphWidget, Node, Edge
w = GraphWidget()
w.nodes = [
    Node(id=0, properties={"label": "Hello World"}),
    Node(id=1, properties={"label": "This is a second node."})
]
w.edges = [
    Edge(start=0, end=1, properties={"label": "knows"})
]
```

For example, see [01_introduction.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/01_introduction.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/01_introduction.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

To map custom properties to visual features, see [Data-driven visualization mappings](#data-driven-visualization-mappings).

### Importing from other graph packages

Aside from passing structured data, you can also import from other graph formats by passing the graph object to the constructor's `graph` kwarg,
or use:

* `w.import_graph(graph_object)`

The import supports the following packages: `neo4j`, `graph_tool`, `igraph`, `networkx`, `pygraphviz`, `rdflib` and `pandas` dataframes.

For example, see

* NetworkX: [13_networkx_import.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/13_networkx_import.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/13_networkx_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* Pandas dataframes: [14_pandas_import.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/14_pandas_import.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/14_pandas_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* PyGraphviz: [15_graphviz_import.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/15_graphviz_import.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/15_graphviz_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* Neo4j: [16_neo4j_import.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/16_neo4j_import.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/16_neo4j_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* iGraph: [17_igraph_import.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/17_igraph_import.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/17_igraph_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* graph-tool: [18_graph-tool_import.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/18_graph-tool_import.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/18_graph-tool_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* RDFLib: [19_rdflib_import.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/19_rdflib_import.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/19_rdflib_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

**Note**<br>
Some graph data structures have special attributes for labels, some don't.
The same goes for other graph properties.
This method and the underlying transformations should be seen as best effort
to provide an easy way to input data into the widget.
For more granular control use nodes and edges properties directly.

## Automatic layout algorithms

There are different layouts available to customize the arrangement of nodes and edges in the graph visualization.

* `graph_layout: Union[Layout, str]`
    * By default, a force-directed layout is applied to the graph. Otherwise, the values of the below table can be used.
    * Preferably set via the [`Layout`](#layout) enum, e.g. `w.graph_layout = Layout.HIERARCHICAL`. Plain strings are also accepted for backwards compatibility.

| Value                      | Description                                                                                                    |
|----------------------------|----------------------------------------------------------------------------------------------------------------|
| `"circular"`               | Arranges nodes in singly cycle and bundles edge paths.                                                         |
| `"circular_straight_line"` | Arranges nodes in singly cycle and uses straight-line edge paths.                                              |
| `"hierarchical"`           | Organizes nodes in hierarchical layers to emphasize directional flow.                                          |
| `"organic"`                | Uses a force-directed algorithm to create a natural, free-form<br> network layout.                             |
| `"interactive_organic"`    | Similar to `ORGANIC` but dynamically adjusts the layout as the user<br>interacts with it.                      |
| `"orthogonal"`             | Positions nodes on a grid with right-angled edges for clear,<br> structured diagrams.                          |
| `"radial"`                 | Places a central node in the middle and arranges others in rings<br> around it to show hierarchy or influence. |
| `"tree"`                   | Displays nodes in a branching tree structure from a defined root node.                                         |
| `"map"`                    | Uses user-defined geo-coordinates to place the nodes on a world map                                            |
| `"orthogonal_edge_router"` | Reroutes edges at right angles to minimize overlap and improve readability.                                    |
| `"organic_edge_router"`    | Smoothly routes edges around obstacles in a natural, curved manner.                                            |
| `"no_layout"`              | Leaves node positions unchanged without applying any automatic layout.                                         |

For example, see [22_layouts.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/22_layouts.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/22_layouts.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

The layouts can also be set through convenience methods on the widget, e.g. `w.hierarchical_layout()`.

For more in-depth information about layout algorithms, see [yFiles SDK – Layout Algorithms](https://www.yfiles.com/the-yfiles-sdk/key-benefits#layout-algorithms).


## Data-driven visualization mappings

You can adjust the graph visualization on an item basis by providing the following mapping functions.
Each mapping is passed the original data object of your original node / edge data, and you need to return
a mapping-specific dict or value to that is reflected in the graph visualization.

To remove a mapping, set the property to `None`, e.g. `w.node_color_mapping = None`. 

The legacy `set_*`, `get_*` and `del_*` methods are deprecated. Use the properties directly instead.

### Property mappings 

Specify what data should be put on the items `properties` field, and therefore considered by the other data mappings

* `node_property_mapping: Optional[Union[str, Callable[[dict], dict]]]`
* `edge_property_mapping: Optional[Union[str, Callable[[dict], dict]]]`

By default, the origin dict for each item is returned.

### Label mappings

Specify the visualized text on each item.

* `node_label_mapping: Optional[Union[str, Callable[[dict], Union[str, LabelStyle]]]]`
* `edge_label_mapping: Optional[Union[str, Callable[[dict], Union[str, LabelStyle]]]]`

Returning a string will first be resolved against the `properties` of the item's dict and if there is no such property 
key the value is used as-is. Alternatively, return a [`LabelStyle`](#labelstyle) dataclass with the following properties 
to have full control over the item's text:

#### Label style dict
* `font: str`: The font used for the label.
* `text: str`: The text that is added to the item.
* `font_size: int`: The text size.
* `font_weight: FontWeight`: The font weight.
* `color: string`: The text color.
* `background_color: str`: A color string that is used as the label's background.
* `position: LabelPosition`: Where the label is placed relatively to the node.
* `maximum_width: int`: The maximum width of the label. By default, the label is clipped at the given size, or wrapped when `wrapping` is set.
* `maximum_height: int`: The maximum height of the label. Clips the label at the given height. May be combined with `wrapping`.
* `wrapping: TextWrapping`: Text wrapping for the label. Must be set in combination with `maximum_width`.
* `text_alignment: TextAlignment`: The horizontal text alignment when `wrapping` is enabled.

For example, see [02a_label_styles_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/02a_label_styles_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/02a_label_styles_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

### Color mappings
Specify the color of each item.
* `node_color_mapping: Optional[Union[str, Callable[[dict], str]]]`
* `edge_color_mapping: Optional[Union[str, Callable[[dict], str]]]`
  
Return any CSS color value (e.g., a color constant, a hex value, a rgb string, etc.).

For example, see [03_color_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/03_color_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/03_color_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

### Node and edge visualization mappings
Specify the visualization properties of nodes and edges by returning a [`NodeStyle`](#nodestyle) / [`EdgeStyle`](#edgestyle) 
dataclass (preferred) or a dict with specific properties.

* `node_styles_mapping: Optional[Union[str, Callable[[dict], NodeStyle]]]`
    * Return a `NodeStyle` with the following, optional properties:
        * `color`: `str`, a CSS color value
        * `image`: `str`, an URL or data URL of the image
        * `shape`: `NodeShape`

* `edge_styles_mapping: Optional[Union[str, Callable[[dict], EdgeStyle]]]`
    * Return an `EdgeStyle` or a dict with the following, optional properties:
        * `color`: `str` (a CSS color value)
        * `directed`: `bool`
        * `thickness`: `float`
        * `dash_style`: `DashStyle` or a dashing string like `"5 10"` or `"5, 10"`

* `edge_thickness_factor_mapping: Optional[Union[str, Callable[[dict], float]]]`
    * Controls the thickness of the edges with a factor that is multiplied to its base size.

* `directed_mapping: Optional[Union[str, Callable[[dict], bool]]]`
    * Allows specifying which edge should be visualized with direction (indicated by an arrow).

For example, see

* [08_styles_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/08_styles_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/08_styles_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* [10_direction_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/10_direction_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/10_direction_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* [11_thickness_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/11_thickness_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/11_thickness_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

### Geometry mappings
Specify the location and/or size of nodes. Note that the location of an item is overwritten from an automatic layout,
unless the `no_layout` option is used.

* `node_scale_factor_mapping: Optional[Union[str, Callable[[dict], float]]]`
    * Controls the node size with a factor that is multiplied to its base size.

* `node_size_mapping: Optional[Union[str, Callable[[int, dict], float]]]`
    * Controls the node size by width and height by returning a tuple `(width, height)`.

* `node_position_mapping: Optional[Union[str, Callable[[dict], Tuple[float, float]]]]`
    * Controls the position of the node by returning a tuple: `(x, y)`.

* `node_layout_mapping: Optional[Union[str, Callable[[dict], Tuple[float, float, float, float]]]]`
    * Controls the bounding box of the nodes (position and size) by returning a 4-tuple: `(x, y, width, height)`.

For example, see

* [04_layout_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/04_layout_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/04_layout_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* [05_size_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/05_size_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/05_size_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* [06_position_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/06_position_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/06_position_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

### Geospatial mapping
Specify a geo-coordinate for the nodes that is used by the geospatial layout option.

* `node_coordinate_mapping: Optional[Union[str, Callable[[dict], Tuple[float, float]]]]`
    * The mapping is supposed to return a tuple of `(latitude, longitude)`.

For example, see [30_leaflet_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/30_leaflet_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/30_leaflet_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

### Hierarchy mappings
Specify which nodes should be grouped together.

* `node_parent_mapping: Optional[Union[str, Callable[[dict], Union[str, int, float]]]]`
    * This mapping does not create new group nodes and just resolves the mapped id against the given dataset.
      It should be used when the group nodes are already **part of** the given dataset.
    * It should return an id for each given node object which is then used as parent group node for this child node. If the parent node does not existing in the dataset, no grouping is created.

* `node_parent_group_mapping: Optional[Union[str, Callable[[dict], Union[str, dict]]]]`
    * This mapping always creates new group nodes based on the given mapping.
      It should be used when the group nodes are **not part of** the given dataset.
    * The returned value must either be a `str` which is used as label and id for the new group node (i.e. nodes with the same mapped `str` are grouped together), or it must be a dict with a mandatory `label` property (return same labels for different nodes defines the group for these nodes) and optional more key-value pairs that are added as properties to the group. These additional properties are also considered when resolving other node mappings (e.g. for the styling of group nodes).
    * Example Snippets
      
```python
w = GraphWidget()
w.nodes = airports
w.edges = flight_paths
# Assuming each node has a "country" property, group all nodes with the same "country" into groups, 
# labeled with the value of the "country" property.
w.node_parent_group_mapping = "country"
display(w)
```

```python
w = GraphWidget()
w.nodes = airports
w.edges = flight_paths
# Assuming each node has a "country" property, group all nodes with the same "country" into groups, 
# and assign additional properties to group nodes that can be mapped e.g. by node_styles_mapping.
w.node_parent_group_mapping = lambda node: {"label": node["properties"]["country"], "color": "#9F4499", "char_count": len(node["properties"]["country"])}
display(w)
```

For example, see [31_nested_graphs.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/31_nested_graphs.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/31_nested_graphs.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

### Heat mapping
Numeric values on nodes and edges may be visualized as a heatmap overlay on the graph visualization.

* `heat_mapping: Optional[Union[str, Callable[[dict], float]]]`
    * The returned heat needs to be normalized in-between `0` and `1`.

For example, see [29_heat_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/29_heat_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/29_heat_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

### Fine-tuning automatic layouts
Some mappings affect specific automatic layouts:

* `node_type_mapping: Optional[Union[str, Callable[[dict], str]]]`
    * Assign a specific "type" string to each item. This affects most of the automatic layouts such that same types are placed adjacent to each other, if possible.
    * See also [Layout with Custom Node Types](https://docs.yworks.com/yfileshtml/dguide/node_types/).

* `node_cell_mapping: Optional[Union[str, Callable[[dict], Tuple[int, int]]]]`
    * Assign a cell tuple `(row, column)` to each node. This information is considered by the hierarchical layout and helps to fine-tune the result, for example, to highlight specific structures of the graph or to convey critical information.

For example, see

* [09_type_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/09_type_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/09_type_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
* "Node-cell mapping" in [v1.9.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/v1.9.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/v1.9.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Edge direction

By default, edges are visualized undirected, i.e., no arrowhead is rendered. This can be changed globally by setting the following property:

* `directed: bool`
    * Specifies whether all edges should be rendered with an arrowhead indicating its direction.

Alternatively, the direction visualization can be specified per edge through the [Node and edge visualization mappings](#node-and-edge-visualization-mappings).

For example, see [10_direction_mapping.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/10_direction_mapping.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/10_direction_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

## Neighborhood

* `neighborhood: Union[int, dict]`
    * Controls the initial neighborhood view settings.
    * Pass an `int` to only set the `max_distance` (number of hops), e.g. `w.neighborhood = 2`.
    * Pass a `dict` with `max_distance` and `selected_nodes` keys to set both, e.g. `w.neighborhood = {"max_distance": 2, "selected_nodes": [2]}`.

For example, see [24_neighborhood.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/24_neighborhood.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/24_neighborhood.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

## Sidebar

The sidebar of the widget provides different panels that can be controlled interactively or programmatically by the following API:

* `sidebar: Union[bool, dict]`
    * Controls the initial sidebar configuration.
    * Pass a `bool` to simply open (`True`) or collapse (`False`) the sidebar, e.g. `w.sidebar = True`.
    * Pass a `dict` with `enabled` or `start_with` keys for full control, e.g. `w.sidebar = {"enabled": True, "start_with": "Search"}`.

Supported values for `start_with` are: `"About"`, `"Search"`, `"Data"`, `"Neighborhood"`

For example, see [23_sidebar.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

## Overview

The graph overview shows the current viewport in relation to the whole graph and allows users to quickly navigate large structures.

* `overview: bool`
    * By default, the overview is expanded unless the widget's width is too small. This behavior can be overwritten by setting the property, e.g. `w.overview = False`.

For example, see [25_overview.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/25_overview.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/25_overview.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

## Selection

The currently selected node and edge dicts can be accessed in the Python cell with the following property:

* `selection: Tuple[List[dict], List[dict]]`
    * Returns a tuple of lists containing the selected nodes and edges, i.e., `nodes, edges = w.selection`.

For example, see [21_selection_export.ipynb](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/21_selection_export.ipynb) <a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/21_selection_export.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>.

## Data classes and enums

The widget exposes a number of dataclasses and enums that can be used instead of plain dictionaries and strings.
They are the **preferred** way to provide structured data and styles because they offer better developer experience
such as code-completion and type-checking. For backwards compatibility, plain dictionaries and strings (for enum
values) are still accepted wherever a dataclass is expected.

All classes below can be imported directly from the `yfiles_jupyter_graphs` module.

### Node

Represents a node in the graph.

| Property     | Type             | Description                        | Default |
|--------------|------------------|------------------------------------|---------|
| `id`         | `str \| int`     | The unique identifier of the node. | -       |
| `properties` | `dict[str, Any]` | Additional properties of the node. | `{}`    |

```python
from yfiles_jupyter_graphs import Node
node = Node(id=0, properties={"label": "Hello", "group": "A"})
```

### Edge

Represents an edge in the graph.

| Property     | Type             | Description                                                                  | Default |
|--------------|------------------|------------------------------------------------------------------------------|---------|
| `start`      | `str \| int`     | The id of the start node.                                                    | -       |
| `end`        | `str \| int`     | The id of the end node.                                                      | -       |
| `id`         | `str \| int`     | Optional. The unique identifier of the edge. Auto-generated if not provided. | uuid    |
| `properties` | `dict[str, Any]` | Additional properties of the edge.                                           | `{}`    |

```python
from yfiles_jupyter_graphs import Edge
edge = Edge(start=0, end=1, properties={"label": "knows"})
```

### NodeStyle

Styling options for nodes, returned by [`node_styles_mapping`](#node-and-edge-visualization-mappings).

| Property | Type                | Description                                            | Default |
|----------|---------------------|--------------------------------------------------------|---------|
| `color`  | `str \| None`       | CSS color value.                                       | `None`  |
| `image`  | `str \| None`       | URL or data URL of the image.                          | `None`  |
| `shape`  | `NodeShape \| None` | The shape of the node (see [`NodeShape`](#nodeshape)). | `None`  |

```python
from yfiles_jupyter_graphs import NodeStyle, NodeShape
w.node_styles_mapping = lambda node: NodeStyle(color="#FF0000", shape=NodeShape.RECTANGLE)
```

#### NodeShape

| Member                       | Value                |
|------------------------------|----------------------|
| `NodeShape.ELLIPSE`          | `"ellipse"`          |
| `NodeShape.HEXAGON`          | `"hexagon"`          |
| `NodeShape.HEXAGON_STANDING` | `"hexagon_standing"` |
| `NodeShape.OCTAGON`          | `"octagon"`          |
| `NodeShape.PILL`             | `"pill"`             |
| `NodeShape.RECTANGLE`        | `"rectangle"`        |
| `NodeShape.ROUND_RECTANGLE`  | `"round_rectangle"`  |
| `NodeShape.TRIANGLE`         | `"triangle"`         |
| `NodeShape.SQUIRCLE`         | `"squircle"`         |

### EdgeStyle

Styling options for edges, returned by [`edge_styles_mapping`](#node-and-edge-visualization-mappings).

| Property     | Type                       | Description                                                                                             | Default |
|--------------|----------------------------|---------------------------------------------------------------------------------------------------------|---------|
| `color`      | `str \| None`              | CSS color value.                                                                                        | `None`  |
| `directed`   | `bool \| None`             | Whether the edge is visualized with an arrowhead.                                                       | `None`  |
| `thickness`  | `float \| None`            | The stroke thickness of the edge.                                                                       | `None`  |
| `dash_style` | `DashStyle \| str \| None` | The dash style (see [`DashStyle`](#dashstyle)). Custom dashing strings like `"5 10"` are also accepted. | `None`  |

```python
from yfiles_jupyter_graphs import EdgeStyle, DashStyle
w.edge_styles_mapping = lambda edge: EdgeStyle(color="#0000FF", directed=True, dash_style=DashStyle.DASH)
```

#### DashStyle

| Member                   | Value            |
|--------------------------|------------------|
| `DashStyle.SOLID`        | `"solid"`        |
| `DashStyle.DASH`         | `"dash"`         |
| `DashStyle.DOT`          | `"dot"`          |
| `DashStyle.DASH_DOT`     | `"dash-dot"`     |
| `DashStyle.DASH_DOT_DOT` | `"dash-dot-dot"` |

### LabelStyle

Styling options for labels, returned by [`node_label_mapping`](#label-mappings) and [`edge_label_mapping`](#label-mappings).

| Property           | Type                    | Description                                                        | Default |
|--------------------|-------------------------|--------------------------------------------------------------------|---------|
| `text`             | `str \| None`           | The text that is added to the item.                                | `None`  |
| `font`             | `str \| None`           | The font used for the label.                                       | `None`  |
| `font_size`        | `int \| None`           | The text size.                                                     | `None`  |
| `font_weight`      | `FontWeight \| None`    | The font weight (see [`FontWeight`](#fontweight)).                 | `None`  |
| `color`            | `str \| None`           | The text color.                                                    | `None`  |
| `background_color` | `str \| None`           | A color string used as the label's background.                     | `None`  |
| `position`         | `LabelPosition \| None` | Where the label is placed (see [`LabelPosition`](#labelposition)). | `None`  |
| `maximum_width`    | `int \| None`           | The maximum width of the label.                                    | `None`  |
| `maximum_height`   | `int \| None`           | The maximum height of the label.                                   | `None`  |
| `wrapping`         | `TextWrapping \| None`  | Text wrapping (see [`TextWrapping`](#textwrapping)).               | `None`  |
| `text_alignment`   | `TextAlignment \| None` | Horizontal text alignment (see [`TextAlignment`](#textalignment)). | `None`  |

```python
from yfiles_jupyter_graphs import LabelStyle, LabelPosition
w.node_label_mapping = lambda node: LabelStyle(text=node["properties"]["label"], position=LabelPosition.SOUTH, color="#FF0000")
```

#### LabelPosition

| Member                  | Value       |
|-------------------------|-------------|
| `LabelPosition.CENTER`  | `"center"`  |
| `LabelPosition.NORTH`   | `"north"`   |
| `LabelPosition.EAST`    | `"east"`    |
| `LabelPosition.SOUTH`   | `"south"`   |
| `LabelPosition.WEST`    | `"west"`    |

#### TextWrapping

| Member                                 | Value                       |
|----------------------------------------|-----------------------------|
| `TextWrapping.NONE`                    | `"none"`                    |
| `TextWrapping.CLIP`                    | `"clip"`                    |
| `TextWrapping.TRIM_CHARACTER`          | `"trim_character"`          |
| `TextWrapping.TRIM_CHARACTER_ELLIPSIS` | `"trim_character_ellipsis"` |
| `TextWrapping.TRIM_WORD`               | `"trim_word"`               |
| `TextWrapping.TRIM_WORD_ELLIPSIS`      | `"trim_word_ellipsis"`      |
| `TextWrapping.WRAP_CHARACTER`          | `"wrap_character"`          |
| `TextWrapping.WRAP_CHARACTER_ELLIPSIS` | `"wrap_character_ellipsis"` |
| `TextWrapping.WRAP_WORD`               | `"wrap_word"`               |
| `TextWrapping.WRAP_WORD_ELLIPSIS`      | `"wrap_word_ellipsis"`      |

#### FontWeight

| Member               | Value       |
|----------------------|-------------|
| `FontWeight.BOLD`    | `"bold"`    |
| `FontWeight.BOLDER`  | `"bolder"`  |
| `FontWeight.NORMAL`  | `"normal"`  |
| `FontWeight.LIGHTER` | `"lighter"` |

#### TextAlignment

| Member                 | Value      |
|------------------------|------------|
| `TextAlignment.CENTER` | `"center"` |
| `TextAlignment.LEFT`   | `"left"`   |
| `TextAlignment.RIGHT`  | `"right"`  |

### Layout

Enum of available automatic layout algorithms, used with [`graph_layout`](#automatic-layout-algorithms).

```python
from yfiles_jupyter_graphs import GraphWidget, Layout
w = GraphWidget()
w.graph_layout = Layout.HIERARCHICAL
```

| Member                          | Value                      |
|---------------------------------|----------------------------|
| `Layout.CIRCULAR`               | `"circular"`               |
| `Layout.CIRCULAR_STRAIGHT_LINE` | `"circular_straight_line"` |
| `Layout.HIERARCHICAL`           | `"hierarchical"`           |
| `Layout.ORGANIC`                | `"organic"`                |
| `Layout.INTERACTIVE_ORGANIC`    | `"interactive_organic"`    |
| `Layout.ORTHOGONAL`             | `"orthogonal"`             |
| `Layout.RADIAL`                 | `"radial"`                 |
| `Layout.TREE`                   | `"tree"`                   |
| `Layout.MAP`                    | `"map"`                    |
| `Layout.ORTHOGONAL_EDGE_ROUTER` | `"orthogonal_edge_router"` |
| `Layout.ORGANIC_EDGE_ROUTER`    | `"organic_edge_router"`    |
| `Layout.NO_LAYOUT`              | `"no_layout"`              |

## Displaying the graph widget

To display the interactive graph widget in the Jupyter notebook, use one of the following methods:

* `show()`
* `display(w)`

For example, see any of the [example notebooks](https://github.com/yWorks/yfiles-jupyter-graphs/tree/main/examples).
