---
title: NetworkX
date: 2021-04-13
author: m0wer
tags: [ 'python', 'networks', 'graphs' ]
---

[NetworkX](https://networkx.org/) is a Python package for the creation,
manipulation, and study of the structure, dynamics, and functions of complex
networks.

# Importing

## Import from Pandas

### Import from edgelist

You need a `DataFrame` containing at least `origin` and `destination` columns.
The rest of the columns, or a selection of them, can be imported as edge
attributes. An input `DataFrame` could look like

| origin | destination | weight | cost |
|--------|-------------|--------|------|
| A      | B           | 2      | 100  |
| A      | C           | 1      | 20   |
| ...    | ...         | ...    | ...  |

To create an `NetworkX.Graph` from it, do


```python
import networkx as nx
import pandas as pd
import matplotlib.pyplot as plt

df = pd.DataFrame({
    "origin": ["A", "A"],
    "destination": ["B", "C"],
    "weight": [2, 1],
    "cost": [100, 20]
})

G = nx.from_pandas_edgelist(df,
                            source="origin",
                            target="destination",
                            edge_attr=["weight", "cost"],
                            create_using=nx.DiGraph())

# Draw it
pos = nx.spring_layout(G, k=10)  # For better example looking
nx.draw(G, pos, with_labels=True)
labels = {e: G.edges[e]["cost"] for e in G.edges}
nx.draw_networkx_edge_labels(G, pos, edge_labels=labels)
plt.show()
```

![NetworkX Graph from edge list](networkx_from_edgelist.png)

Only add `create_using=nx.DiGraph()` if you want the result to be a directed
graph, otherwise it will be an undirected one by default.

### Add node attributes from Series

You can add node attributes to an existing graph from a Pandas Series with_labels


```python
nx.set_node_attributes(G, pd.Series(nodes.gender, index=nodes.node).to_dict(), 'gender')
```

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
