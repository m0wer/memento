---
title: Jupyter Notebook/Lab
date: 2021-04-14
author: m0wer
tags: [ 'python', 'jupyter' ]
---

[Jupyter Notebook/Lab](https://jupyter.org/) is an open-source web application
that allows you to create and share documents that contain live code,
equations, visualizations and narrative text. It can be used for R and for
Python, among others.

# Extensions

## jupyter-server-proxy

[Jupyter Server Proxy](https://jupyter-server-proxy.readthedocs.io/) lets you
run arbitrary external processes (such as RStudio, Shiny Server, syncthing,
PostgreSQL, etc) alongside your notebook, and provide authenticated web access
to them.

Once installed, you'll be able to access arbitrary hosts and ports at
`<notebook-base>/proxy/<host>:<port>`.

### Installation

First, install the required server extension

```bash
jupyter serverextension enable --sys-prefix jupyter_server_proxy
```

then, install the Python package

```bash
pip install jupyter-server-proxy
```

and you're ready to go.

# Libraries

## jupyter-dash

[plotly/jupyter-dash](https://github.com/plotly/jupyter-dash) is a library
that makes it easy to develop Plotly Dash apps interactively from within
Jupyter environments.

## Installation

```bash
pip install jupyter-dash
```

## Usage

In a Jupyter Notebook, run this example application

```python
import plotly.express as px
from jupyter_dash import JupyterDash
JupyterDash.infer_jupyter_proxy_config()
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output
# Load Data
df = px.data.tips()
# Build App
app = JupyterDash(__name__)
app.layout = html.Div([
    html.H1("JupyterDash Demo"),
    dcc.Graph(id='graph'),
    html.Label([
        "colorscale",
        dcc.Dropdown(
            id='colorscale-dropdown', clearable=False,
            value='plasma', options=[
                {'label': c, 'value': c}
                for c in px.colors.named_colorscales()
            ])
    ]),
])
# Define callback to update graph
@app.callback(
    Output('graph', 'figure'),
    [Input("colorscale-dropdown", "value")]
)
def update_figure(colorscale):
    return px.scatter(
        df, x="total_bill", y="tip", color="size",
        color_continuous_scale=colorscale,
        render_mode="webgl", title="Tips"
    )
# Run app and display result inline in the notebook
app.run_server(mode='inline')
```

`JupyterDash.infer_jupyter_proxy_config()` is needed if the Jupyter server is
not accessible directly, and needs the [jupyter-server-proxy](#jupyter-server-proxy)
extension to be installed.
