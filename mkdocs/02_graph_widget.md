# GraphWidget
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Class

Inherits from [ipywidgets.DOMWidget](https://github.com/jupyter-widgets/ipywidgets/blob/master/python/ipywidgets/ipywidgets/widgets/domwidget.py)

**The main widget class.**

To be used in jupyter-notebook or jupyter-lab.

### Example

```Python
from yfiles_jupyter_graphs import GraphWidget
w = GraphWidget()
w.show()
```

See notebooks for more examples.

### Notes

Nodes and edges properties should be constructed recursively with basic python types otherwise {de-}serializers will fail.

## Properties

### <a id="nodes_property" href="#nodes_property"><code>nodes: typing.List[typing.Dict]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data structure.

**`def get_nodes()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the nodes traitlets property.

**Notes**

This function acts as an alias for using GraphWidget.nodes property e.g. `w.nodes == w.get_nodes()`.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `nodes` | `typing.List[typing.Dict]` | Each node has the keys `id: int` and `properties: typing.Dict`. It might include keys that are not set directly, see (default) node mappings for details. |

**`def set_nodes(nodes)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the nodes traitlets property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `nodes` | `typing.List[typing.Dict]` | Each node should have the keys `id: int` and `properties: typing.Dict`. Properties should be constructed recursively with basic python types, otherwise {de-}serializers will fail. |

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: w.set_nodes([
            {'id': 0, 'properties': {'label': 'Hello World'}},
            {'id': 1, 'properties': {'label': 'This is a second node.'}}
        ])
```

**Notes**

This function acts as an alias for using GraphWidget.nodes property e.g. `w.nodes = [{...}]` has the same effect as using `w.set_nodes([{...}])`.

&nbsp;

### <a id="edges_property" href="#edges_property"><code>edges: typing.List[typing.Dict]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data structure.

**`def get_edges()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the edges traitlets property.

**Notes**

This function acts as an alias for using GraphWidget.edges property e.g. `w.edges == w.get_edges()` is `true`.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edges` | `typing.List[typing.Dict]` | Each edge has the keys `id: int`, `start: int`, `end: int` and `properties: typing.Dict`. It might include keys that are not set directly, see (default) edge mappings for details. |

**`def set_edges(edges)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the edges traitlets property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edges` | `typing.List[typing.Dict]` | Each edge should have the keys `id: int`, `start: int`, `end:int` and `properties: typing.Dict`. Ids for start and end should be among used node ids, otherwise the edge does not appear. Properties should be constructed recursively with basic python types, otherwise {de-}serializers will fail. |

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: w.set_edges([
            {'id': 0, 'start': 0, 'end': 1, 'properties': {'label': 'edge between first and second node'}}
        ])
```
**Notes**

This function acts as an alias for using GraphWidget.edges property e.g. `w.edges = [{...}]` has the same effect as using `w.set_edges([{...}])`.

&nbsp;

### <a id="directed_property" href="#directed_property"><code>directed: bool</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Graph wide flag for edge type.

**`def get_directed()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the directed traitlets property.

**Notes**

This function acts as an alias for using GraphWidget.directed property e.g. `w.directed == w.get_directed()` is `true`.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `directed` | `bool` | Whether the graph is interpreted as directed. |

**`def set_directed(directed)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the directed traitlets property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `directed` | `bool` | Whether the graph is interpreted as directed. |

**Notes**

This function acts as an alias for using GraphWidget.directed property e.g. `w.directed = x` has the same effect as using `w.set_directed(x)`.

&nbsp;

### <a id="graph_layout_property" href="#graph_layout_property"><code>graph_layout: typing.Dict</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Choose an algorithm for positioning nodes and/or edges.

**`def get_graph_layout()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the graph layout traitlet property.

**Notes**

This function acts as an alias for using GraphWidget.graph_layout property\
e.g. `w.graph_layout == w.get_graph_layout()` is `true`.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `graph_layout` | `typing.Dict` | Returned dict has keys algorithm: str and options: dict, however options are empty because the algorithms use default settings from yFiles library. |

**`def set_graph_layout(algorithm)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Choose graph layout.

Currently the algorithms use default settings from yFiles library.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `algorithm` | `str` | Specify graph layout (or edge router) algorithm. Available algorithms are: ["circular", "hierarchic", "organic", "orthogonal", "radial", "tree", "orthogonal_edge_router", "organic_edge_router"] |
| `**kwargs` | `typing.Dict` (optional) | Extra arguments to algorithm configuration, currently ignored. |

**Notes**

This function acts as an alias for using GraphWidget.graph_layout property\
e.g. `w.graph_layout = 'organic'` has the same effect as using `w.set_graph_layout('organic')`.\
Setting `w.graph_layout = {'algorithm': 'organic', 'options': {}}` works as well,\
which corresponds to using value given through the associated getter.\
In case you want to use the edge routers\
you should set a custom node position mapping as well.

See [yFiles docs](https://docs.yworks.com/yfileshtml/#/dguide/layout-summary) for more details about the algorithms.

&nbsp;

### <a id="neighborhood_property" href="#neighborhood_property"><code>neighborhood: typing.Dict</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Control neighborhood view component.

**`def get_neighborhood()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the neighborhood traitlets property.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `neighborhood` | `typing.Dict` | Returned dict has keys max_distance: int and selected_nodes: list, a list of node ids. |

**`def set_neighborhood(max_distance, selected_nodes)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Specify the neighborhood view in the widget.

The number of hops and focused nodes can be chosen.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `max_distance` | `int` | Set the maximum distance between selected and included nodes. If there are multiple paths to one (or multiple) selected nodes, the smallest path length is considered for this threshold. |
| `selected_nodes` | `typing.List` (optional) | Choose a list of node ids that are highlighted in both main and neighborhood component. They act as starting points for neighborhood calculation. |

**Notes**

This function acts as an alias for using GraphWidget.neighborhood property.\
You can assign values by `w.neighborhood = {'max_distance': 2, 'selected_nodes':[2]}`\
or `w.set_neighborhood(2, [2])`, both are equivalent.\
The short form `w.neighborhood = 3` sets only the max_distance variable\
and resets the selected nodes.

&nbsp;

### <a id="sidebar_property" href="#sidebar_property"><code>sidebar: typing.Dict</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Control sidebar component.

**`def get_sidebar()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the sidebar traitlets property.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `sidebar` | `typing.Dict` | Returned dict has keys enabled: bool and start_with: str, whereat first one indicates open or closed sidebar and second one indicates start panel on widget show. |

**`def set_sidebar(enabled, start_with)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Specify the appearance of the sidebar in the widget.

Can be used to collapse sidebar or start with any panel.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `enabled` | `bool` | Whether to open or collapse sidebar at widget startup. |
| `start_with` | `str` | The start panel identifier. Available are 'Neighborhood', 'Data', 'Search' and 'About' (the default). |

**Notes**

This function acts as an alias for using GraphWidget.sidebar property.\
You can assign values by `w.sidebar = {'enabled': True, 'start_with': 'Search'}`\
or `w.set_sidebar(True, 'Search')`, both are equivalent.\
The short form `w.sidebar = True` sets only the enabled variable\
and resets the start_with back to the default.

&nbsp;

### <a id="overview_property" href="#overview_property"><code>overview: bool</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Control overview component.

**`def get_overview()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the overview traitlets property.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `overview` | `bool` | Indicates open or closed overview state. A value of None means that a specific behaviour based on widget layout is followed. |

**`def set_overview(enabled)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Specify the appearance of the overview component in the widget.

Can be used to force open overview in case of a small widget layout or\
force collapsed overview in case of large widget layout.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `enabled` | `bool` | Whether to open or collapse overview at widget startup. |

&nbsp;

### <a id="node_label_mapping_property" href="#node_label_mapping_property"><code>node_label_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of node label on a per node basis.

**`def get_node_label_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the node label mapping property.

**Notes**

If no mapping is explicitly set, [`default_node_label_mapping`](#default_node_label_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_label_mapping` | `Union[callable, str]` | A function that produces node labels or the name of the property to use for binding. |

**`def set_node_label_mapping(node_label_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the node label mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_label_mapping` | `Union[callable, str]` | A function that produces node labels or the name of the property to use for binding. The function should have the same signature as `default_node_label_mapping` e.g. take in an index and node dictionary and return a string.|

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_label_mapping(index: int, node: dict):
         ...
In [4]: w.set_node_label_mapping(custom_node_label_mapping)
```

**`def del_node_label_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the name property.

Remove a custom node label mapping.

&nbsp;

### <a id="edge_label_mapping_property" href="#edge_label_mapping_property"><code>edge_label_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of edge label on a per edge basis.

**`def get_edge_label_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the edge label mapping property.

**Notes**

If no mapping is explicitly set, [`default_edge_label_mapping`](#default_edge_label_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edge_label_mapping` | `Union[callable, str]` |  A function that produces edge labels or the name of the property to use for binding.|

**`def set_edge_label_mapping(edge_label_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the edge label mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edge_label_mapping` | `Union[callable, str]` | A function that produces edge labels or the name of the property to use for binding. The funtion should have the same signature as `default_edge_label_mapping` e.g. take in an index and edge dictionary and return a string. |

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_edge_label_mapping(index: int, node: dict):
         ...
In [4]: w.set_edge_label_mapping(custom_edge_label_mapping)
```

**`def del_edge_label_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the edge label mapping property.

Remove a custom edge label mapping.

&nbsp;

### <a id="node_property_mapping_property" href="#node_property_mapping_property"><code>node_property_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of node properties on a per node basis.

**`def get_node_property_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the node property mapping property.

**Notes**

If no mapping is explicitly set, [`default_node_property_mapping`](#default_node_property_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_property_mapping` | `Union[callable, str]` | A function that produces node properties or the name of the property to use for binding. |

**`def set_node_property_mapping(node_property_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the node property mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_property_mapping` | `Union[callable, str]` | A function that produces node properties or the name of the property to use for binding. The function should have the same signature as `default_node_property_mapping` e.g. take in an index and node dictionary and return a dictionary. |

**Notes**

Properties are changed inplace by this mapping.

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_property_mapping(index: int, node: dict):
         ...
In [4]: w.set_node_property_mapping(custom_node_property_mapping)
```

**`def del_node_property_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the node property mapping property.

Remove a custom node property mapping.

&nbsp;

### <a id="edge_property_mapping_property" href="#edge_property_mapping_property"><code>edge_property_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of edge properties on a per edge basis.

**`def get_edge_property_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the edge property mapping property.

**Notes**

If no mapping is explicitly set, [`default_edge_property_mapping`](#default_edge_property_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edge_property_mapping` | `Union[callable, str]` | A function that produces edge properties or the name of the property to use for binding. |

**`def set_edge_property_mapping(edge_property_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the edge property mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edge_property_mapping` | `Union[callable, str]` | A function that produces edge properties or the name of the property to use for binding. The function should have the same signature as `default_edge_property_mapping` e.g. take in an index and edge dictionary and return a dictionary. |

**Notes**

Properties are changed inplace by this mapping.

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_edge_property_mapping(index: int, node: dict):
         ...
In [4]: w.set_edge_property_mapping(custom_edge_property_mapping)
```

**`def del_edge_property_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the edge property mapping property.

Remove a custom edge property mapping.

&nbsp;

### <a id="node_color_mapping_property" href="#node_color_mapping_property"><code>node_color_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of node color on a per node basis.

**`def get_node_color_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the node color mapping property.

**Notes**

If no mapping is explicitly set, [`default_node_color_mapping`](#default_node_color_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_color_mapping` | `Union[callable, str]` | A function that produces node colors or the name of the property to use for binding. |

**`def set_node_color_mapping(node_color_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the node color mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_color_mapping` | `Union[callable, str]` | A function that produces node colors or the name of the property to use for binding. The function should have the same signature as `default_node_color_mapping` e.g. take in an index and node dictionary and return a string. |

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_color_mapping(index: int, node: dict):
         ...
In [4]: w.set_node_color_mapping(custom_node_color_mapping)
```

**`def del_node_color_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the node color mapping property.

Remove a custom node color mapping.

&nbsp;

### <a id="node_styles_mapping_property" href="#node_styles_mapping_property"><code>node_styles_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of node styles on a per node basis.

**`def get_node_styles_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the node styles mapping property.

**Notes**

If no mapping is explicitly set, [`default_node_styles_mapping`](#default_node_styles_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_styles_mapping` | `Union[callable, str]` | A function that produces node styles or the name of the property to use for binding. |

**`def set_node_styles_mapping(node_styles_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the node styles mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_styles_mapping` | `Union[callable, str]` | A function that produces node styles or the name of the property to use for binding. The function should have the same signature as `default_node_styles_mapping` e.g. take in an index and node dictionary and return a string. |

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_styles_mapping(index: int, node: dict):
         ...
In [4]: w.set_node_styles_mapping(custom_node_styles_mapping)
```

**`def del_node_styles_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the node styles mapping property.

Remove a custom node styles mapping.

&nbsp;

### <a id="edge_color_mapping_property" href="#edge_color_mapping_property"><code>edge_color_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of edge color on a per edge basis.

**`def get_edge_color_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the edge color mapping property.

**Notes**

If no mapping is explicitly set, [`default_edge_color_mapping`](#default_edge_color_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edge_color_mapping` | `Union[callable, str]` | A function that produces edge colors or the name of the property to use for binding. |

**`def set_edge_color_mapping(edge_color_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the edge color mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edge_color_mapping` | `Union[callable, str]` | A function that produces edge colors or the name of the property to use for binding. The function should have the same signature as `default_edge_color_mapping` e.g. take in an index and edge dictionary and return a string. |

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_edge_color_mapping(index: int, node: dict):
         ...
In [4]: w.set_edge_color_mapping(custom_edge_color_mapping)
```

**`def del_edge_color_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the edge color mapping property.

Remove a custom edge color mapping.

&nbsp;

### <a id="node_scale_factor_mapping_property" href="#node_scale_factor_mapping_property"><code>node_scale_factor_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of node scale factor on a per node basis.

**`def get_node_scale_factor_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the node scale factor mapping property.

**Notes**

If no mapping is explicitly set, [`default_node_scale_factor_mapping`](#default_node_scale_factor_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_scale_factor_mapping` | `Union[callable, str]` | A function that produces node scale factor or the name of the property to use for binding. |

**`def set_node_scale_factor_mapping(node_scale_factor_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the node scale factor mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_scale_factor_mapping` | `Union[callable, str]` | A function that produces node scale factors or the name of the property to use for binding. The function should have the same signature as `default_node_scale_factor_mapping` e.g. take in an index and node dictionary and return a positive float. |

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_scale_factor_mapping(index: int, node: dict):
         ...
In [4]: w.set_node_scale_factor_mapping(custom_node_scale_factor_mapping)
```

**`def del_node_scale_factor_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the node scale factor mapping property.

Remove a custom node scale factor mapping.

&nbsp;

### <a id="edge_thickness_factor_mapping_property" href="#edge_thickness_factor_mapping_property"><code>edge_thickness_factor_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of edge thickness factor on a per edge basis.

**`def get_edge_thickness_factor_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the edge thickness factor mapping property.

**Notes**

If no mapping is explicitly set, [`default_edge_thickness_factor_mapping`](#default_edge_thickness_factor_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edge_thickness_factor_mapping` | `Union[callable, str]` | A function that produces edge thickness factors or the name of the property to use for binding. |

**`def set_edge_thickness_factor_mapping(edge_thickness_factor_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the edge thickness factor mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edge_thickness_factor_mapping` | `Union[callable, str]` | A function that produces edge thickness factors or the name of the property to use for binding. The function should have the same signature as `default_edge_thickness_factor_mapping` e.g. take in an index and edge dictionary and return a positive float. |

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_edge_thickness_factor_mapping(index: int, node: dict):
         ...
In [4]: w.set_edge_thickness_factor_mapping(custom_edge_thickness_factor_mapping)
```

**`def del_edge_thickness_factor_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the edge thickness factor mapping property.

Remove a custom edge thickness factor mapping.

&nbsp;

### <a id="node_type_mapping_property" href="#node_type_mapping_property"><code>node_type_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of node type on a per node basis.

**`def get_node_type_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the node type mapping property.

**Notes**

If no mapping is explicitly set, [`default_node_type_mapping`](#default_node_type_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_type_mapping` | `Union[callable, str]` | A function that produces node types or the name of the property to use for binding. |

**`def set_node_type_mapping(node_type_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the node type mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_type_mapping` | `Union[callable, str]` | A function that produces node types or the name of the property to use for binding. The function should have the same signature as `default_node_type_mapping` e.g. take in an index and node dictionary and return a bool/int/float or str value. |

**Notes**

Node types give more information for some layout algorithms.

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_type_mapping(index: int, node: dict):
         ...
In [4]: w.set_node_type_mapping(custom_node_type_mapping)
```

**References**

[Layout with Custom Node Types](https://docs.yworks.com/yfileshtml/#/dguide/layout-summary#node_types)


**`def del_node_type_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the node type mapping property.

Remove a custom node type mapping.

&nbsp;

### <a id="node_position_mapping_property" href="#node_position_mapping_property"><code>node_position_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change of node position on a per node basis.

**`def get_node_position_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the node position mapping property.

**Notes**

If no mapping is explicitly set, [`default_node_position_mapping`](#default_node_position_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_position_mapping` | `Union[callable, str]` | A function that produces node positions or the name of the property to use for binding. |

**`def set_node_position_mapping(node_position_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the node position mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_position_mapping` | `Union[callable, str]` | A function that produces node positions or the name of the property to use for binding. The function should have the same signature as `default_node_position_mapping` e.g. take in an index and node dictionary and return a float 2-tuple. |

**Notes**

Only edge router algorithms consider node positions,\
all other algorithms calculate node positions themselves.

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_position_mapping(index: int, node: dict):
         ...
In [4]: w.set_node_position_mapping(custom_node_position_mapping)
```

**`def del_node_position_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the node position mapping property.

Remove a custom node position mapping.

&nbsp;

### <a id="directed_mapping_property" href="#directed_mapping_property"><code>directed_mapping: Union[callable, str]</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Data dependent change if an edge is directed or not.

**`def get_directed_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Getter for the directed mapping property.

**Notes**

If no mapping is explicitly set, [`default_directed_mapping`](#default_directed_mapping) is returned.

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `directed_mapping` | `Union[callable, str]` | A function that produces edge directions or the name of the property to use for binding. |

**`def set_directed_mapping(directed_mapping)`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Setter for the directed mapping property.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `directed_mapping` | `Union[callable, str]` | A function that produces edge directions or the name of the property to use for binding. The function should have the same signature as `default_directed_mapping` e.g. take in an index and edge dictionary and return a boolean value. |

**Example**
```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_directed_mapping(index: int, node: dict):
         ...
In [4]: w.set_directed_mapping(custom_directed_mapping)
```

**`def del_directed_mapping()`**<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Deleter for the directed mapping property.

Remove a custom directed mapping.

&nbsp;

## Methods

### <a id="init_method" href="#init_method"><code>def __init__(widget_layout = None, overview_enabled = None, context_start_with = '')</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; GraphWidget constructor.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `widget_layout` | `ipywidgets.Layout` (optional) | Can be used to specify general widget appearance through css attributes. See [references](#References) for a link to their documentation and available keywords. |
| `overview_enabled` | `bool` (optional) | Enable graph overview component. Default behaviour depends on cell width. |
| `context_start_with` | `str` (optional) | Specify context tab name to start with that tab opened. Default behaviour is open with *About* dialog. Use `None` to start with closed sidebar. Available are *Neighborhood*, *Data*, *Search* and *About*. |

&nbsp;

### <a id="show_method" href="#show_method"><code>def show()</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Display widget in Jupyter.

Same as using single object reference in cell directly.

**Notes**

Mappings will only be applied shortly before showing the widget.

&nbsp;

### <a id="import_graph_method" href="#import_graph_method"><code>def import_graph(graph)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Import a graph object defined in an external module.

Sets the [`nodes`](#nodes_property), [`edges`](#edges_property) and [`directed`](#directed_property) traitlets properties \
with information extracted from the graph object. \
See [graph importers](#graph_importers) for object specific transformation details.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `graph` | `networkx.{Multi}{Di}Graph \| graph_tool.Graph \| igraph.Graph \| pygraphviz.AGraph` | The graph data structure. |

**Example**
```Python
In [1]: from networkx import florentine_families_graph
In [2]: from yfiles_jupyter_graphs import GraphWidget
In [3]: w = GraphWidget()
In [4]: w.import_graph(florentine_families_graph())
```

**Notes**

Some graph data structures have special attributes for labels, some don't.\
Same goes for other graph properties.\
This method and the underlying transformations should be seen as best effort\
to provide an easy way to input data into the widget.\
For more granular control use nodes and edges properties directly.

&nbsp;

### <a id="circular_layout_method" href="#circular_layout_method"><code>def circular_layout()</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Alias for GraphWidget.<a href="#graph_layout_property">graph_layout</a= "circular".

See [yFiles circular layout guide](https://docs.yworks.com/yfileshtml/#/dguide/layout-summary#layout_styles-circular)
for more details about this specific algorithm.

&nbsp;

### <a id="hierarchic_layout_method" href="#hierarchic_layout_method"><code>def hierarchic_layout()</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Alias for GraphWidget.<a href="#graph_layout_property">graph_layout</a= "hierarchic".

See [yFiles hierarchic layout guide](https://docs.yworks.com/yfileshtml/#/dguide/layout-summary#layout_styles-hierarchical)
for more details about this specific algorithm.

&nbsp;

### <a id="organic_layout_method" href="#organic_layout_method"><code>def organic_layout()</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Alias for GraphWidget.<a href="#graph_layout_property">graph_layout</a= "organic".

See [yFiles organic layout guide](https://docs.yworks.com/yfileshtml/#/dguide/layout-summary#layout_styles-organic)
for more details about this specific algorithm.

&nbsp;

### <a id="orthogonal_layout_method" href="#orthogonal_layout_method"><code>def orthogonal_layout()</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Alias for GraphWidget.<a href="#graph_layout_property">graph_layout</a= "orthogonal".

See [yFiles orthogonal layout guide](https://docs.yworks.com/yfileshtml/#/dguide/layout-summary#layout_styles-orthogonal)
for more details about this specific algorithm.

&nbsp;

### <a id="radial_layout_method" href="#radial_layout_method"><code>def radial_layout()</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Alias for GraphWidget.<a href="#graph_layout_property">graph_layout</a= "radial".

See [yFiles radial layout guide](https://docs.yworks.com/yfileshtml/#/dguide/layout-summary#layout_styles-radial)
for more details about this specific algorithm.

&nbsp;

### <a id="tree_layout_method" href="#tree_layout_method"><code>def tree_layout()</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Alias for GraphWidget.<a href="#graph_layout_property">graph_layout</a= "tree".

See [yFiles tree layout guide](https://docs.yworks.com/yfileshtml/#/dguide/layout-summary#layout_styles-tree)
for more details about this specific algorithm.

&nbsp;

### <a id="orthogonal_edge_router_method" href="#orthogonal_edge_router_method"><code>def orthogonal_edge_router()</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Alias for GraphWidget.<a href="#graph_layout_property">graph_layout</a= "orthogonal_edge_router".

See [yFiles orthogonal edge router guide](https://docs.yworks.com/yfileshtml/#/dguide/layout-summary#layout_styles-polyline_router)
for more details about this specific algorithm.

&nbsp;

### <a id="organic_edge_router_method" href="#organic_edge_router_method"><code>def organic_edge_router()</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Alias for GraphWidget.<a href="#graph_layout_property">graph_layout</a= "organic_edge_router".

See [yFiles organic edge router guide](https://docs.yworks.com/yfileshtml/#/dguide/layout-summary#layout_styles-organic_router)
for more details about this specific algorithm.

&nbsp;

### <a id="default_element_label_mapping" href="#default_element_label_mapping"><code>def default_element_label_mapping(index, element)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default property mapping for graph elements.

The default label mapping for graph elements.

Element (dict) should have key properties which itself should be a dict.\
Then one of the following values (in descending priority) is used as label:
- properties["label"]
- properties["yf_label"]

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `index` | `int` | Position in corresponding nodes or edges list. |
| `element` | `typing.Dict` | Can be both node or edge. |

**Notes**

This is the default value for the {[node](#node_label_mapping_property)|[edge](#edge_label_mapping_property)}_label_mapping property.\
Can be 'overwritten' by setting the property with a function of the same signature.

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_element_label_mapping(index: int, element: typing.Dict):
         ...
In [4]: w.set_{node|edge}_label_mapping(custom_element_label_mapping)
```

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `label` | `str` | The node or edge label. |

&nbsp;

### <a id="default_node_label_mapping" href="#default_node_label_mapping"><code>def default_node_label_mapping(index, node)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default label mapping for nodes.

See [`default_element_label_mapping`](#default_element_label_mapping).

&nbsp;

### <a id="default_edge_label_mapping" href="#default_edge_label_mapping"><code>def default_edge_label_mapping(index, edge)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default label mapping for edges.

See [`default_element_label_mapping`](#default_element_label_mapping).

&nbsp;

### <a id="default_element_property_mapping" href="#default_element_property_mapping"><code>def default_element_property_mapping(index, element)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default property mapping for graph elements.

Simply selects the properties value of element dictionary.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `index` | `int` | Position in corresponding nodes or edges list. |
| `element` | `typing.Dict` | Can be both node or edge. |

**Notes**

This is the default value for the {[node](#node_property_mapping_property)|[edge](#edge_property_mapping_property)}_property_mapping property.\
Can be 'overwritten' by setting the property with a function of the same signature.

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_element_property_mapping(index: int, element: typing.Dict):
         ...
In [4]: w.set_{node|edge}_property_mapping(custom_element_property_mapping)
```

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `properties` | `typing.Dict` | The node or edge properties. |

&nbsp;

### <a id="default_node_property_mapping" href="#default_node_property_mapping"><code>def default_node_property_mapping(index, node)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default property mapping for nodes.

See [`default_element_property_mapping`](#default_element_property_mapping).

&nbsp;

### <a id="default_edge_property_mapping" href="#default_edge_property_mapping"><code>def default_edge_property_mapping(index, edge)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default property mapping for edges.

See [`default_element_property_mapping`](#default_element_property_mapping).

&nbsp;

### <a id="default_node_color_mapping" href="#default_node_color_mapping"><code>def default_node_color_mapping(index, node)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default color mapping for nodes.

Provides constant value of '#17bebb' for all nodes.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `index` | `int` | Position in nodes list. |
| `node` | `typing.Dict` | |

**Notes**

This is the default value for the [`node_color_mapping`](#node_color_mapping_property) property.\
Can be 'overwritten' by setting the property with a function of the same signature.

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_color_mapping(index: int, node: typing.Dict):
          ...
In [4]: w.set_node_color_mapping(custom_node_color_mapping)
```

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `color` | `str` | CSS color value. |

**References**

[css color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value)

[yFiles docs Fill api](https://docs.yworks.com/yfileshtml/#/api/Fill)

&nbsp;

### <a id="default_node_styles_mapping" href="#default_node_styles_mapping"><code>def default_node_styles_mapping(index, node)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default styles mapping for nodes.

Provides constant value of {} for all nodes.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `index` | `int` | Position in nodes list. |
| `node` | `typing.Dict` | |

**Notes**

This is the default value for the [`node_styles_mapping`](#node_styles_mapping_property) property.\
Can be 'overwritten' by setting the property with a function of the same signature.

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_styles_mapping(index: int, node: typing.Dict):
          ...
In [4]: w.set_node_styles_mapping(custom_node_styles_mapping)
```

**Returns**

| Name | Type | Description                                                                  |
| ----------- | ----------- |------------------------------------------------------------------------------|
| `styles` | `typing.Dict` | A `Dict` with mappings for style attributes. See below for supported values. |

Supported style attributes in the return `Dict`:
```Python
can contain the following key-value-pairs:
    "color": str
        css color value
    "shape": str
        possible values: 'ellipse', 'hexagon', 'hexagon2', 'octagon', 'pill', 'rectangle', 'round-rectangle' or 'triangle'
    "image": str
        url or data URL of the image
```

**References**

[css color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value)

[Data URL](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs)

&nbsp;

### <a id="default_edge_color_mapping" href="#default_edge_color_mapping"><code>def default_edge_color_mapping(index, edge)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default color mapping for edges.

Provides constant value of '#094c4b' for all edges.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `index` | `int` | Position in edges list. |
| `edge` | `typing.Dict` | |

**Notes**

This is the default value for the [`edge_color_mapping`](#edge_color_mapping_property) property.\
Can be 'overwritten' by setting the property with a function of the same signature.

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_edge_color_mapping(index: int, edge: typing.Dict):
         ...
In [4]: w.set_edge_color_mapping(custom_edge_color_mapping)
```

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `color` | `str` | CSS color value. |

**References**

[css color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value)

[yFiles docs Fill api](https://docs.yworks.com/yfileshtml/#/api/Fill)

&nbsp;

### <a id="default_node_scale_factor_mapping" href="#default_node_scale_factor_mapping"><code>def default_node_scale_factor_mapping(index, node)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default scale factor mapping for nodes.

Provides constant value of 1.0 for all nodes.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `index` | `int` | Position in nodes list. |
| `node` | `typing.Dict` | |

**Notes**

This is the default value for the [`node_scale_factor_mapping`](#node_scale_factor_mapping_property) property.\
Can be 'overwritten' by setting the property with a function of the same signature.

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_scale_factor_mapping(index: int, node: typing.Dict):
         ...
In [4]: w.set_node_scale_factor_mapping(custom_node_scale_factor_mapping)
```

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_scale_factor` | `float` | Positive scale factor. |

&nbsp;

### <a id="default_edge_thickness_factor_mapping" href="#default_edge_thickness_factor_mapping"><code>def default_edge_thickness_factor_mapping(index, edge)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default thickness factor mapping for edges.

Provides constant value of 1.0 for all edges.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `index` | `int` | Position in edges list. |
| `edge` | `typing.Dict` | |

**Notes**

This is the default value for the [`edge_thickness_factor_mapping`](#edge_thickness_factor_mapping_property) property.\
Can be 'overwritten' by setting the property with a function of the same signature.

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_edge_thickness_factor_mapping(index: int, edge: typing.Dict):
         ...
In [4]: w.set_edge_thickness_factor_mapping(custom_edge_thickness_factor_mapping)
```

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `edge_thickness_factor` | `float` | Positive thickness factor. |

&nbsp;

### <a id="default_node_type_mapping" href="#default_node_type_mapping"><code>def default_node_type_mapping(index, node)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default type mapping for nodes.

Provides constant value of `None` for all nodes.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `index` | `int` | Position in nodes list. |
| `node` | `typing.Dict` | |

**Notes**

This is the default value for the [`node_type_mapping`](#node_type_mapping_property) property.\
Can be 'overwritten' by setting the property with a function of the same signature.

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_type_mapping(index: int, node: typing.Dict):
         ...
In [4]: w.set_node_type_mapping(custom_node_type_mapping)
```

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_type` | `None` | Node Type. |

&nbsp;

### <a id="default_node_position_mapping" href="#default_node_position_mapping"><code>def default_node_position_mapping(index, node)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default position mapping for nodes.

Provides constant value of [0.0, 0.0] for all nodes.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `index` | `int` | Position in nodes list. |
| `node` | `typing.Dict` | |

**Notes**

This is the default value for the [`node_position_mapping`](#node_position_mapping_property) property.\
Can be 'overwritten' by setting the property with a function of the same signature.

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_node_position_mapping(index: int, node: typing.Dict):
         ...
In [4]: w.set_node_position_mapping(custom_node_position_mapping)
```

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `node_position` | `float 2-tuple` | Position in euclidian plane. |

&nbsp;

### <a id="default_directed_mapping_method" href="#default_directed_mapping_method"><code>def default_directed_mapping(index, edge)</code></a><br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; The default directed mapping for edges.

Uses the graph wide directed attribute for all edges.

**Parameters**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `index` | `int` | Position in edges list. |
| `edge` | `typing.Dict` | |

**Notes**

This is the default value for the [`directed_mapping`](#directed_mapping_property) property.\
Can be 'overwritten' by setting the property with a function of the same signature.

**Example**

```Python
In [1]: from yfiles_jupyter_graphs import GraphWidget
In [2]: w = GraphWidget()
In [3]: def custom_directed_mapping(index: int, edge: typing.Dict):
         ...
In [4]: w.set_directed_mapping(custom_directed_mapping)
```

**Returns**

| Name | Type | Description |
| ----------- | ----------- | ----------- |
| `directed` | `bool` | Whether the edge is directed or not. |
