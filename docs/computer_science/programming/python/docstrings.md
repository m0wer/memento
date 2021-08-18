---
title: Docstrings
date: 2021-08-18
author: m0wer
tags: [ 'documentation' ]
---

A docstring is a string literal that occurs as the first statement in a module,
function, class, or method definition. Such a docstring becomes the `__doc__`
special attribute of that object. See
[PEP 257](https://www.python.org/dev/peps/pep-0257/)

Example docstring for a function:

```python
def connect_to_next_port(self, minimum: int) -> int:
  """Connects to the next available port.

      Args:
        minimum: A port value greater or equal to 1024.

      Returns:
        The new minimum port.

      Raises:
        ConnectionError: If no available port is found.
  """
```
