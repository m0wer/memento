---
title: Python typing
date: 2021-04-14
author: m0wer
tags: [ 'python' ]
---

# Typing

Since Python 3.5, type hints are supported. Note that the Python runtime does
not enforce function and variable type annotations but they can be used by
third party tools such as type checkers, IDEs, linters, etc.

## Usage

When defining a function, the syntax to specify the type of an argument and its
default value, which is optional, is
`{arg_name}: {arg_type} = {arg_default_value}`. The return type can also by
specified. Let's see an example:

```python
def greeting(name: str) -> str:
    return 'Hello ' + name
```

### Type aliases

A type alias is defined by assigning the type to the alias. For example:

```python
import pandas as pd
import networkx as nx

## Type aliases
Series = pd.core.series.Series
DataFrame = pd.core.frame.DataFrame
Graph = nx.classes.graph.Graph
```

## Types

Common types from `typing`:

* `Type[Class]`: Accepts instances of the `Class` and the `Class` itself.
* `Awaitable`: Promise/Future.

## Common problems

### F821 undefined name when class method return type is the class name

Since the class is not defined yet, to use it as the return type that a class
method returns you need to:

```bash
from __future__ import annotations
```
