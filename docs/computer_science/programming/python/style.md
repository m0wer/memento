---
title: Python Style
date: 2021-04-09
tags: [ 'programming', 'python', 'style' ]
---

# PEP-8

PEP-8 is a style guide for Python code.

## Indentation

Use 4 spaces as the TAB length as stated by
[pep-8](https://www.python.org/dev/peps/pep-0008/#indentation)-

### Long strings

Implicit concatenation might be the cleanest solution:

```python
s = "this is my really, really, really, really, really, really," \
    " really long string that I'd like to shorten."
```

# Packages

## pprint

`pprint` is a Python module provides a capability to “pretty-print” arbitrary
Python data structures in a form which can be used as input to the interpreter.

```python
import pprint

things = [a,b,c]

pprint.pprint(things)
```

The documentation can be found
[here](https://docs.python.org/3/library/pprint.html).
