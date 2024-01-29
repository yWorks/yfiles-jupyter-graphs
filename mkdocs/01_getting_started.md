# Getting started

## Requirements
- [python](https://www.python.org/) >= 3.6
- [jupyter](https://jupyter.org/install) notebook or lab
- [ipywidgets](https://github.com/jupyter-widgets/ipywidgets) >= 7.6.0

## Installation

If you already have Jupyter installed, just `pip install` the prebuilt extension from the [Python Package Index](https://pypi.org/).

```bash
pip install yfiles_jupyter_graphs
```

If you want to start clean and get a fresh new Jupyter Lab with the widget readily installed and available, you can use [`docker`](https://www.docker.com/), too:

Form a shell, create a docker image that contains all that is required:

```bash
mkdir yfiles-jupyter && cd yfiles-jupyter
echo -e "FROM jupyter/scipy-notebook\nRUN pip install yfiles-jupyter-graphs" > Dockerfile
docker build -t yfiles-jupyter-graphs-on-docker .
```

(the above has been tested successfully with `scipy-notebook:lab-3.4.7` and `yfiles-jupyter-graphs==1.2.1`), but we want to make sure that it will also work with  upcoming versions - file an issue if it doesn't work for you!)

You can then create a fresh new instance of your server from this image like so:

```bash
docker run -it -p 8888:8888 --name yfiles-jupyter yfiles-jupyter-graphs-on-docker
```

## Usage

In a notebook which has the wiget installed in the server, in a Python cell, you can then do this:

## Usage
```python
"""Execute in jupyter notebook or jupyter lab"""
from yfiles_jupyter_graphs import GraphWidget
# shows empty widget
GraphWidget()
```