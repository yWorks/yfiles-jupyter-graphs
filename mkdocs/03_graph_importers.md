# Graph Importers

Used by the [`GraphWidget.import_graph`](#import_graph_method) method.

Included here mainly for understanding features rather than showing how to use them directly.

## class GraphToolsGraphImporter

Class for importing graphs from the [graph tool](https://graph-tool.skewed.de/) package.

Notes

- Graph properties are ignored.
- Nodes and edges are identified by index.
- Node and edge properties are extracted from corresponding property maps.
- Default values for unset properties are used, due to the way graph tool properties work.

## class IGraphGraphImporter

Class for importing graphs from the [igraph](https://igraph.org/python/) package.

Notes

- Nodes and edges are identified by index attribute.
- Node and edge properties are provided through attributes method.
- Edges are determined by source and target attribute.

## class NetworkxGraphImporter

Class for importing graphs from the [networkx](https://networkx.org/) package.

Notes

- Graph attributes are ignored.
- Node identifiers are saved under property key *label* (or *yf_label* if key *label* already exists).
- Node identifiers have to be unique.
- Subgraphs (graph as node, see [here](https://networkx.org/documentation/stable/tutorial.html#using-the-graph-constructors)) are not supported.

## class PyGraphvizGraphImporter

Class for importing graphs from the [pygraphviz](https://pygraphviz.github.io/) package.

Notes

- Graph attributes are ignored.
- Node names are saved under property key *label* (or *yf_label* if key *label* already exists).
- Node names have to be unique.
- Unspecified default node/edge attributes are empty (and shown as null in data viewer).
- Subgraphs are dissolved.