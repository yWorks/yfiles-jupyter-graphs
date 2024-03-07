# Graph Importers

Used by the [`GraphWidget.import_graph`](#import_graph_method) method.

## Neo4j Importer

Importer for graphs from [Neo4j](https://pypi.org/project/neo4j/).

### Notes

- By default, the widget displays the node's label and the edge's type as text. This may be adjusted by setting a different label-mapping, e.g., see [02_label_mapping](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/02_label_mapping.ipynb).
- Node labels are combined with ':' and added as 'label' property on the item
- Node and relationship properties are available on the graph item's `properties`.
- Each node label or relationship type is assigned a specific color.

### Example

First, create a Neo4j driver with access to your database
```python
from neo4j import GraphDatabase
from yfiles_jupyter_graphs import GraphWidget

NEO4J_URI      = "neo4j+s://demo.neo4jlabs.com" 
NEO4J_USERNAME = "movies"
NEO4J_PASSWORD = "movies"

# create a neo4j session to run queries
driver = GraphDatabase.driver(uri = NEO4J_URI, auth = (NEO4J_USERNAME, NEO4J_PASSWORD), database = 'movies')
session = driver.session()
```

This driver can then be used to query a result graph by importing the result with the yFiles Graphs for Jupyter widget:
```python
# directly show the graph resulting from the given Cypher query
def showGraph(cypher: str):
    widget = GraphWidget(graph = session.run(cypher).graph()) 
    
    # potentially configure some mappings of the widget...
    def node_label_mapping(node):
        properties = node['properties']
        return properties.get('name', properties.get('label', '<unlabeled>')) 
    
    w.node_label_mapping = node_label_mapping
    
    display(widget)
    
# display a Cypher query as graph
showGraph("MATCH (s)-[r]->(t) RETURN s,r,t LIMIT 20")
```
See also this [Jupyter Notebook](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/16_neo4j_import.ipynb)
<a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/16_neo4j_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Graph Tool Importer

Importer for graphs from the [graph tool](https://graph-tool.skewed.de/) package.

### Notes

- Graph properties are ignored.
- Nodes and edges are identified by index.
- Node and edge properties are extracted from corresponding property maps.
- Default values for unset properties are used, due to the way graph tool properties work.

### Example

See this [Jupyter Notebook](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/18_graph-tool_import.ipynb)
<a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/18_graph-tool_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## igraph Importer 

Importer for graphs from the [igraph](https://igraph.org/python/) package.

### Notes

- Nodes and edges are identified by index attribute.
- Node and edge properties are provided through attributes method.
- Edges are determined by source and target attribute.

### Example

See this [Jupyter Notebook](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/17_igraph_import.ipynb)
<a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/17_igraph_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Networkx Importer

Importer for graphs from the [networkx](https://networkx.org/) package.

### Notes

- Graph attributes are ignored.
- Node identifiers are saved under property key *label* (or *yf_label* if key *label* already exists).
- Node identifiers have to be unique.
- Subgraphs (graph as node, see [here](https://networkx.org/documentation/stable/tutorial.html#using-the-graph-constructors)) are not supported.

### Example

See this [Jupyter Notebook](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/13_networkx_import.ipynb)
<a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/13_networkx_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## PyGraphviz Importer

Importer for graphs from the [pygraphviz](https://pygraphviz.github.io/) package.

### Notes

- Graph attributes are ignored.
- Node names are saved under property key *label* (or *yf_label* if key *label* already exists).
- Node names have to be unique.
- Unspecified default node/edge attributes are empty (and shown as null in data viewer).
- Subgraphs are dissolved.

### Example

See this [Jupyter Notebook](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/15_graphviz_import.ipynb)
<a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/15_graphviz_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
