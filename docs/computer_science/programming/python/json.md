---
title: json Python module
date: 2021-05-17
author: m0wer
tags: [ 'json', 'python' ]
---

[`json`](https://docs.python.org/3/library/json.html?highlight=json#module-json)
is a JSON encoder and decoder for Python.

# Usage

## Load a file

Use `json.load`. You can specify the file encoding if necessary.

```python
import json

with open('{path}', encoding='utf-8') as f:
    data = json.load(f)
```

### Load a file with multiple JSON objects

`json.load` expects a single JSON object, so if your file has a JSON object per
line, load the objects of each line with `json.loads` that expects an `str`
object instead of a file.

```python
import json

data = []
with open('{path}') as f:
    for line in f:
        data.append(json.loads(line))
```
