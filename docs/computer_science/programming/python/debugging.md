---
title: Python debugging
date: 2021-04-09
author: m0wer
tags: [ 'python', 'programming'  ]
---

Use `pdb` as follows

```python
import pdb

# code

pdb.set_trace()
 ```

 This will stop the program execution once the breakpoint (`pdb.set_trace()`)
 is reached. Then, an interactive console while appear.

[pythonconquerstheuniverse](https://pythonconquerstheuniverse.wordpress.com/2009/09/10/debugging-in-python/)
is a short tutorial to `pdb` and [this is the official
documentaion](https://docs.python.org/3/library/pdb.html).
