<p align="center">
  <img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/yfiles-jupyter-graphs-logo.svg" alt="yFiles Graphs for Jupyter logo" width="400" style="max-width: 400px"/>
</p>

[![PyPI - Version](https://img.shields.io/pypi/v/yfiles-jupyter-graphs?label=pypi%20package&color=%234c1)](https://pypi.org/project/yfiles-jupyter-graphs/)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/yfiles-jupyter-graphs)](https://pypi.org/project/yfiles-jupyter-graphs/)
[![Docs - Latest](https://img.shields.io/badge/docs-latest-green?color=%234c1)](https://yworks.github.io/yfiles-jupyter-graphs/02_graph_widget/)
[![Python Versions](https://img.shields.io/pypi/pyversions/yfiles-jupyter-graphs.svg)](https://pypi.org/project/yfiles-jupyter-graphs/)
[![License](https://img.shields.io/badge/license-See%20LICENSE.md-blue)](LICENSE.md)

> Using Neo4j, Kuzu, or SPARQL? Use our dedicated integrations instead:
> [Neo4j](https://github.com/yWorks/yfiles-jupyter-graphs-for-neo4j) ·
> [Kuzu](https://github.com/yWorks/yfiles-jupyter-graphs-for-kuzu) ·
> [SPARQL](https://github.com/yWorks/yfiles-jupyter-graphs-for-sparql)

A graph visualization widget for Jupyter Notebook and JupyterLab powered by
[yFiles for HTML](https://www.yfiles.com/the-yfiles-sdk/web/yfiles-for-html?utm_campaign=yfiles4jupyter&utm_source=github&utm_medium=readme).

Visualize graphs from many sources out of the box:
- [NetworkX](https://networkx.org/) ✅
- [igraph](https://igraph.org/python/) ✅
- [neo4j](https://pypi.org/project/neo4j/) ✅ (use the dedicated [neo4j package](https://github.com/yWorks/yfiles-jupyter-graphs-for-neo4j))
- [pygraphviz](https://pygraphviz.github.io/) ✅
- Native Python dicts/lists ✅

Many more formats are supported via [NetworkX imports](https://networkx.org/documentation/stable/reference/readwrite/index.html#reading-and-writing-graphs).

[![yFiles Graphs for Jupyter](https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/yfiles-jupyter-graphs.gif)](https://player.vimeo.com/video/715615671)

Try the [showcase](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/feature_showcase.ipynb) notebook in Colab: https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/showcase.ipynb

---

## Key Features
- Fast, production-grade graph rendering (yFiles engine)
- Multiple automatic layouts (hierarchical, organic, circular, ...)
- Data-driven styling (colors, sizes, labels, ...) from node/edge attributes
- Sidebars for search, data inspection, and neighborhood exploration
- Heatmaps and map visualization

## Choose your path
There are extensions built on top of `yfiles-jupyter-graphs` that provide tailored APIs and convenient data mapping for their respective ecosystems:

- If you work with Neo4j: use [yfiles-jupyter-graphs-for-neo4j](https://github.com/yWorks/yfiles-jupyter-graphs-for-neo4j)
- If you work with Kuzu: use [yfiles-jupyter-graphs-for-kuzu](https://github.com/yWorks/yfiles-jupyter-graphs-for-kuzu)
- If you query via SPARQL: use [yfiles-jupyter-graphs-for-sparql](https://github.com/yWorks/yfiles-jupyter-graphs-for-sparql)

Otherwise, continue below with `yfiles-jupyter-graphs`.

## Where it runs
- [JupyterLab or Jupyter Notebook](https://jupyter.org/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Google Colab](https://colab.research.google.com/)
- [Gemini Enterprise Agent Platform](https://cloud.google.com/products/gemini-enterprise-agent-platform)
- [Managed Service for Apache Spark](https://cloud.google.com/products/managed-service-for-apache-spark)
- [Azure Machine Learning Studio Notebooks](https://azure.microsoft.com/en-us/products/machine-learning/)
- [Amazon SageMaker](https://aws.amazon.com/sagemaker/)
- [Kaggle](https://www.kaggle.com)
- Just try it in your preferred platform for Jupyter notebooks

## AI Coding Assistant
Working with an AI coding agent? Our [agent guide](agent-guide.md) contains instructions and best practices for coding agents.

**Example start prompt:**
> Read the instructions at https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/refs/heads/main/agent-guide.md. 
> Then, create a new Jupyter notebook that step-by-step explores the <data-file-path> and visualizes it using yfiles-jupyter-graphs. 
> Be creative and design visualizations that highlight interesting insights and aspects of the data.

---

## Install

Prerequisites:
- [python](https://www.python.org/) >= 3.7
- [jupyter](https://jupyter.org/install) notebook or lab
- [ipywidgets](https://github.com/jupyter-widgets/ipywidgets) >= 7.6.0

```bash
pip install yfiles-jupyter-graphs
```

> Important: When installing from inside a notebook, prefer `%pip install yfiles-jupyter-graphs` over `!pip install` to
> ensure the package is installed into the running kernel’s environment.

### Docker (optional)
If you want to start with a clean Jupyter environment that has the widget preinstalled:

```bash
mkdir yfiles-jupyter && cd yfiles-jupyter
echo -e "FROM jupyter/scipy-notebook\nRUN pip install yfiles-jupyter-graphs" > Dockerfile
docker build -t yfiles-jupyter-graphs-on-docker .
docker run -it -p 8888:8888 --name yfiles-jupyter yfiles-jupyter-graphs-on-docker
```

> This approach has been verified with `scipy-notebook:lab-3.4.7` and `yfiles-jupyter-graphs==1.2.1`.
> If you encounter issues with a newer image, please open an issue.

## Quickstart
Display a simple graph:

```python
from yfiles_jupyter_graphs import GraphWidget, Node, Edge
w = GraphWidget(
    nodes=[
        Node(id=0, properties={"firstName": "Alpha", "label": "Person A"}),
        Node(id=1, properties={"firstName": "Bravo", "label": "Person B"}),
        Node(id=2, properties={"firstName": "Charlie", "label": "Person C", "has_hat": False}),
        Node(id=3, properties={"firstName": "Delta", "label": "Person D", "likes_pizza": True})
    ],
    edges=[
        Edge(start=0, end=1, properties={"since": "1992", "label": "knows"}),
        Edge(start=1, end=3, properties={"label": "knows", "since": "1992"}),
        Edge(start=2, end=3, properties={"label": "knows", "since": "1992"}),
        Edge(start=0, end=2, properties={"label": "knows", "since": 234})
    ],
    directed=True
)
display(w)
```

Use the toolbar and sidebar to inspect data, search graph, explore neighborhood and change layouts.

### Next steps
- Check out [more examples](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/00_toc.ipynb) for the different features.
- Jump directly to the API [documentation](https://yworks.github.io/yfiles-jupyter-graphs/02_graph_widget/).

## Feature Gallery
<table>
  <tr>
    <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/28_little-alchemy_example.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/neighborhood.png" title="See Node Neighborhood" alt="neighborhood sidebar"></a>
    <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/28_little-alchemy_example.ipynb">See Node Neighborhood</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/28_little-alchemy_example.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
    <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/22_layouts.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/layouts.png" title="Choose Graph Layout" alt="layouts"></a>
    <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/22_layouts.ipynb">Choose Graph Layout</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/22_layouts.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
  </tr>
  <tr>
    <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/feature_showcase.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/data.png" title="Investigate Nodes and Edges Data" alt="data sidebar"></a>
    <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/feature_showcase.ipynb">Investigate Nodes or Edges Data</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/feature_showcase.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
    <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/search.png" title="Search for Nodes or Edges" alt="search sidebar"></a>
    <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb">Search for Nodes or Edges</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
  </tr>
  <tr>
    <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/13_networkx_import.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/importer.png" title="Import Graph Data" alt="importer"></a>
    <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/13_networkx_import.ipynb">Import Graph Data</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/13_networkx_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
    <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/v1.10.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/data_driven_visualization.png" title="Make Data Dependent Property Changes" alt="element color mapping"></a>
    <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/v1.10.ipynb">Make Data Dependent Property Changes</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/v1.10.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
  </tr>
  <tr>
    <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/29_heat_mapping.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/heat_mapping.png" title="Define a heatmap background" alt="heat mapping"></a>
    <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/29_heat_mapping.ipynb">Define a Heatmap Background</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/29_heat_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
    <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/30_leaflet_mapping.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/leaflet_map.png" title="Use a Map background" alt="leaflet mapping"></a>
    <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/30_leaflet_mapping.ipynb">Use a Map Background</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/30_leaflet_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
  </tr>
  <tr>
    <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/31_nested_graphs.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/nesting.png" title="Visualize nested data" alt="nested graph"></a>
    <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/31_nested_graphs.ipynb">Visualize nested data</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/31_nested_graphs.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
  </tr>
</table>

## Documentation
- [API and usage docs](https://yworks.github.io/yfiles-jupyter-graphs/02_graph_widget/)
- [Example Notebooks](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/00_toc.ipynb)

## Code of Conduct
This project is governed by the [Code of Conduct](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/CODE_OF_CONDUCT.md).
By participating, you are expected to uphold this code.
Please report unacceptable behavior to [contact@yworks.com](mailto:contact@yworks.com).

## Feedback
This widget is by no means perfect.
If you find something is not working as expected
we are glad to receive an issue report from you.
Please make sure to [search for existing issues](https://github.com/yWorks/yfiles-jupyter-graphs/search?q=is%3Aissue+repo%3AyWorks%2Fyfiles-jupyter-graphs&type=issues) first
and check if the issue is not an unsupported feature or known issue.
If you did not find anything related, report a new issue with necessary information.
Please also provide a clear and descriptive title and stick to the issue templates.
See [issues](https://github.com/yWorks/yfiles-jupyter-graphs/issues).

## License
See [LICENSE.md](LICENSE.md) for license information.

### Dependencies
- [yFiles for HTML](https://www.yfiles.com/the-yfiles-sdk/web/yfiles-for-html)
- [@jupyter-widgets/base](https://github.com/jupyter-widgets/ipywidgets)
- [@mdi/js](https://github.com/Templarian/MaterialDesign-JS)
- [Leaflet](https://leafletjs.com/)
- [tinycolor2]([https://github.com/scttcper/tinycolor](https://github.com/bgrins/TinyColor))
- [Vue](https://vuejs.org/)
- [vue-json-viewer](https://github.com/chenfengjw163/vue-json-viewer)
