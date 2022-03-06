# Union-find data structure

In computer science, a disjoint-set data structure, also called a union–find
data structure or merge–find set, is a data structure that stores a collection
of disjoint (non-overlapping) sets.

It can be used to store the connected components of an undirected graph.

An example could be:

```text

0   1---2   3---4
|       |   |   |
|       |   |   |
5---6   7   8   9
```

* *N* is the number of nodes. Equals to *10* in the example.

The data structure should support the following operations:

* **initialize()**: Set the initial state of the graph.
* **find(p, q)**: Are nodes **p** and **q** connected?
* **union(p,q)**: Connect nodes **p** and **q**.

Notation: bold for nodes (**p**), cursive for values (*0*) and monospace for
code (`a == 1`).

## Solutions

### Quick-find

We could store the information in an array `id` of size *N*. This array stores
integers that represent group identifiers, so two nodes are connected if they
are assigned to the same group (connected component).

For the example:

| **Index** | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|-----------|---|---|---|---|---|---|---|---|---|---|
| **Value** | 0 | 1 | 1 | 2 | 2 | 0 | 0 | 1 | 2 | 2 |

Implementation of the operations:

* **initialize**: $O(N)$. Set all values to their index (so that each node starts
  alone).
* **find**: $O(1)$. `id[p] == id[q]`.
* **union**: $O(N)$. Change all values equal to *id[q]* to *id[p]*. For example
  to connect **0** and **1** we could need to change the value of nodes **1**,
  **2** and **7** from *1* to *0*.

### Quick-union

Trees of nodes. Store the id of the parent.


Implementation of the operations:

* **initialize**: $O(N)$. Set all values to their index (so that each node starts
  alone).
* **find**: $O(N)$. We have to find the root node of each and check if they match.
* **union**: $O(N)$. Find the root nodes of each and make one of them child of
  the other.

### Weighted quick-union

An improvement over the previous algorithm that choose which tree to put under
in the union operation. By putting the smallest depth tree under the other it
is guaranteed that find and union operations would have complexity
$O(\log_2{N})$.

The algorithm can be further improved by enabling path compresion, which
consists in assigning the root node to child nodes that we find on our way
of finding the root node. This makes the complexity of find and union almost
linear ($O(N)$) in practice.
