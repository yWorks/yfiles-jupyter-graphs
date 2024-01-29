# Key activation

yFiles Graphs for Jupyter is allow-listed on well-known domains like

- [JupyterLab or Jupyter Notebook](https://jupyter.org/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Google Colaboratory](https://colab.research.google.com/)
- [Google Vertex AI Workbench](https://cloud.google.com/vertex-ai)
- [Google Dataproc](https://cloud.google.com/dataproc)
- [Azure Machine Learning Studio Notebooks](https://azure.microsoft.com/en-us/products/machine-learning/)
- [Amazon SageMaker](https://aws.amazon.com/sagemaker/)

and

- `localhost`
- `127.0.0.1`

## Unknown domains

If your domain is unknown to the widget, you will see a popup in the widget that states that it runs on an unknown
domain.

The widget's popup provides a button with which you can continue using yFiles Graphs for Jupyter anyway.

If you think the widget should also be allow-listed on the domain you are running it on, or if you need a specific
activation license for your domain, please get in touch with us 
by [email](mailto:contact@yworks.com?subject=yFiles%20Graphs%20For%20Jupyter%20-%20Domain%20license%20request) or 
on [GitHub](https://github.com/yWorks/yfiles-jupyter-graphs/discussions/).

## Obtaining a domain specific license 

Please get in touch with us 
by [email](mailto:contact@yworks.com?subject=yFiles%20Graphs%20For%20Jupyter%20-%20Domain%20license%20request) if 
you require a specific activation key for your domain.

## Using a license Key

To use a specific activation license, provide it as `license` parameter to the `GraphWidget` constructor:

```python
w = GraphWidget(license={
  "id": "6440496d-b481-49a5-a824-78d591e590b4",
  "domains": [
    "my.domain.com"
  ],
  "expiry": "2024-01-05",
  "version": "1.0",
  "signature": "8214787cc5f7e2bf25f4a25e43f9d7e9d482c..."
})
```