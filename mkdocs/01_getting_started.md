# Getting started

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
