---
title: NetworkX
date: 2021-04-13
author: m0wer
tags: [ 'python', 'networks', 'graphs' ]
---

[NetworkX](https://networkx.org/) is a Python package for the creation,
manipulation, and study of the structure, dynamics, and functions of complex
networks.

# Exporting

## Export to Gephi

NetworkX graphs can be easily exported to [GEXF File Format](https://gephi.org/gexf/format/),
which is supported by [Gephi](https://gephi.org/). To do so,

```python
import networkx as nx
G = nx.Graph()
nx.write_gexf(G, '{name}.gexf')
```

I had some issues exporting a graph that was created from Pandas. I could only
export it correctly when I left only the `weight` edge attribute.
