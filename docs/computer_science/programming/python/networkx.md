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

# Generators

## Ego graph

To generate the ego graph of a node from an existing graph, you can use
[networkx.generators.ego.ego_graph](https://networkx.org/documentation/stable/reference/generated/networkx.generators.ego.ego_graph.html?highlight=ego_graph#networkx.generators.ego.ego_graph).

```python
networkx.generators.ego.ego_graph(G, n, radius=1, center=True, undirected=False, distance=None)
```

## Undirected graph from directed

Use `networkx.DiGraph.to_undirected(reciprocal=False, as_view=False)`. Set
`reciprocal=True` if you want to keep only the edges that appear in both
directions in the original digraph.

## Subgraph filtering nodes and edges

To get a subgraph of another by filtering nodes and or edges, use
`networkx.classes.graphviews.subgraph_view(G, filter_node=<function no_filter>, filter_edge=<function no_filter>)`.

The functions will get the node name or the edge name only (without attributes)
so keep it in mind while writing the filtering function because you won't be
able to access the node or edge attributes directly.

Example:

```python
import networkx as nx

G = nx.path_graph(6)
G[3][4]["cross_me"] = False

def filter_edge(n1, n2):
    return G[n1][n2].get("cross_me", True)

view = nx.subgraph_view(G, filter_edge=filter_edge)
view.edges()
```

Which returns `EdgeView([(0, 1), (1, 2), (2, 3), (4, 5)])`.
