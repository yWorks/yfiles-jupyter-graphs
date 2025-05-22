<p align="center">
    <img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/yfiles-jupyter-graphs-logo.svg" alt='yFiles Graphs for Jupyter logo'  width="400px" style='max-width: 400px'>
</p>

[![PyPI - Version](https://img.shields.io/pypi/v/yfiles-jupyter-graphs?label=pypi%20package&color=%234c1)](https://pypi.org/project/yfiles-jupyter-graphs/) [![PyPI - Downloads](https://img.shields.io/pypi/dm/yfiles-jupyter-graphs)](https://pypi.org/project/yfiles-jupyter-graphs/) [![Docs - Latest](https://img.shields.io/badge/docs-latest-green?color=%234c1)](https://yworks.github.io/yfiles-jupyter-graphs/)

A graph diagram visualization widget for Jupyter Notebooks and Labs powered by [yFiles for HTML](https://www.yfiles.com/the-yfiles-sdk/web/yfiles-for-html?utm_campaign=yfiles4jupyter&utm_source=github&utm_medium=readme).

Easily visualize graphs from various sources: [Networkx](https://networkx.org/)✅, [igraph](https://igraph.org/python/)✅, [neo4j](https://pypi.org/project/neo4j/)✅, [pygraphviz](https://pygraphviz.github.io/)✅, and any structured Python dictionaries and lists. Many more formats supported indirectly via [Networkx imports](https://networkx.org/documentation/stable/reference/readwrite/index.html#reading-and-writing-graphs)!

The widget is supported in the default Jupyter environments, but also in other environments like VS Code or Google Colab.

[![yFiles Graphs for Jupyter](https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/yfiles-jupyter-graphs.gif)](https://player.vimeo.com/video/715615671)

Try the [Showcase](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/showcase.ipynb) notebook on Google Colab [here](https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/feature-releases/showcase.ipynb). Or see the simple [Introduction](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/01_introduction.ipynb)
notebook.

## `yfiles-jupyter-graphs-for-neo4j`

For working with Neo4j databases, we
built [yfiles-jupyter-graphs-for-neo4j](https://github.com/yWorks/yfiles-jupyter-graphs-for-neo4j/), an open-source
extension on top of `yfiles-jupyter-graphs`. This extension provides an easier Python interface for the
driver and allows direct configuration of data mappings depending on the label or type of the node or relationship.

So if you are planning to use the extension with Neo4j databases, consider
using [yfiles-jupyter-graphs-for-neo4j](https://github.com/yWorks/yfiles-jupyter-graphs-for-neo4j/).

## `yfiles-jupyter-graphs-for-kuzu`

For working with Kuzu databases, we
built [yfiles-jupyter-graphs-for-kuzu](https://github.com/yWorks/yfiles-jupyter-graphs-for-kuzu/), an open-source
extension on top of `yfiles-jupyter-graphs`. This extension provides a specifically tailored API for easier and more
domain specific usage in Kuzu databases (see [Kuzu integration guide](https://docs.kuzudb.com/visualization/third-party-integrations/yfiles/)).

## `yfiles-jupyter-graphs-for-sparql`

For working with RDF databases and SPARQL queries, we built
[yfiles-jupyter-graphs-for-sparql](https://github.com/yWorks/yfiles-jupyter-graphs-for-sparql/), an open-source
extension on top of `yfiles-jupyter-graphs`. This extension provides a specifically tailored API for easier and more
domain specific usage in RDF databases with SPARQL.

## Supported Environments
- [JupyterLab or Jupyter Notebook](https://jupyter.org/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Google Colaboratory](https://colab.research.google.com/)
- [Google Vertex AI Workbench](https://cloud.google.com/vertex-ai)
- [Google Dataproc](https://cloud.google.com/dataproc)
- [Azure Machine Learning Studio Notebooks](https://azure.microsoft.com/en-us/products/machine-learning/)
- [Amazon SageMaker](https://aws.amazon.com/sagemaker/)
- [Kaggle](https://www.kaggle.com)
- Just try it in your preferred platform for Jupyter notebooks

## Requirements
- [python](https://www.python.org/) >= 3.6
- [jupyter](https://jupyter.org/install) notebook or lab
- [ipywidgets](https://github.com/jupyter-widgets/ipywidgets) >= 7.6.0

## Installation

If you already have Jupyter installed, just `pip install` the prebuilt extension from the [Python Package Index](https://pypi.org/).

```bash
pip install yfiles_jupyter_graphs
```
> [!IMPORTANT]  
> To install `yfiles_jupyter_graphs` from within a Jupyter Notebook cell, use `%pip` instead of `!pip` to ensure that it
> is installed in the correct Python environment.

If you want to start clean and get a fresh new Jupyter Lab with the widget readily installed and available, you can use [`docker`](https://www.docker.com/), too:

From a shell, create a docker image that contains all that is required:

```bash
mkdir yfiles-jupyter && cd yfiles-jupyter
echo -e "FROM jupyter/scipy-notebook\nRUN pip install yfiles-jupyter-graphs" > Dockerfile
docker build -t yfiles-jupyter-graphs-on-docker .
```

(the above has been tested successfully with `scipy-notebook:lab-3.4.7` and `yfiles-jupyter-graphs==1.2.1`), but we want to make sure that it will also work with upcoming versions - file an issue if it doesn't work for you!)

You can then create a fresh new instance of your server from this image like so:

```bash
docker run -it -p 8888:8888 --name yfiles-jupyter yfiles-jupyter-graphs-on-docker
```

## Usage

In a notebook which has the widget installed in the server, in a Python cell, you can then do this:

```python
"""Execute in jupyter notebook or jupyter lab"""
from yfiles_jupyter_graphs import GraphWidget
# shows empty widget
GraphWidget()
```

You can find the full documentation [here](https://yworks.github.io/yfiles-jupyter-graphs/).

## Features
<table>
    <tr>
        <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/28_little-alchemy_example.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/neighborhood.png" title="See Node Neighborhood" alt="neighborhood sidebar"></a>
        <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/28_little-alchemy_example.ipynb">See Node Neighborhood</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/28_little-alchemy_example.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
        <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/22_layouts.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/layouts.png" title="Choose Graph Layout" alt="layouts"></a>
        <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/22_layouts.ipynb">Choose Graph Layout</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/22_layouts.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
    </tr>
    <tr>
        <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/data.png" title="Investigate Nodes and Edges Data" alt="data sidebar"></a>
        <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb">Investigate Nodes or Edges Data</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
        <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/search.png" title="Search for Nodes or Edges" alt="search sidebar"></a>
        <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb">Search for Nodes or Edges</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/23_sidebar.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
    </tr>
    <tr>
        <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/13_networkx_import.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/importer.png" title="Import Graph Data" alt="importer"></a>
        <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/13_networkx_import.ipynb">Import Graph Data</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/13_networkx_import.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
        <td><a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/03_color_mapping.ipynb"><img src="https://raw.githubusercontent.com/yWorks/yfiles-jupyter-graphs/main/screenshots/element_color_mapping.png" title="Make Data Dependent Property Changes" alt="element color mapping"></a>
        <a href="https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/03_color_mapping.ipynb">Make Data Dependent Property Changes</a><br><a target="_blank" href="https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/03_color_mapping.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a></td>
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

For example code look [here](https://github.com/yWorks/yfiles-jupyter-graphs/tree/master/examples).

### Google Colab Examples
You can try the [example notebooks](https://github.com/yWorks/yfiles-jupyter-graphs/tree/master/examples) in Google Colab by
opening GitHub notebook URL: `https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/<notebook.ipynb>`.

For example the [Introduction](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/examples/01_introduction.ipynb) notebook: <br>
https://colab.research.google.com/github/yWorks/yfiles-jupyter-graphs/blob/main/examples/01_introduction.ipynb

## Documentation
You can find the documentation [here](https://yworks.github.io/yfiles-jupyter-graphs/).

## Code of Conduct
This project and everyone participating in it is governed by the [Code of Conduct](https://github.com/yWorks/yfiles-jupyter-graphs/blob/master/CODE_OF_CONDUCT.md).
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

## Dependencies
- [yFiles for HTML](https://www.yfiles.com/the-yfiles-sdk/web/yfiles-for-html)
- [@ctrl/tinycolor](https://github.com/scttcper/tinycolor)
- [@jupyter-widgets/base](https://github.com/jupyter-widgets/ipywidgets)
- [@mdi/js](https://github.com/Templarian/MaterialDesign-JS)
- [Vue](https://vuejs.org/)
- [vue-json-viewer](https://github.com/chenfengjw163/vue-json-viewer)

## License
See [LICENSE](https://github.com/yWorks/yfiles-jupyter-graphs/blob/main/LICENSE.md) file.
