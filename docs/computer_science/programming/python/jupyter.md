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
