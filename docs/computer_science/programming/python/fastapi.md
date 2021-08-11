---
title: FastAPI
date: 2021-08-11
author: m0wer
tags: [ 'api', 'http' ]
---

[FastAPI](https://fastapi.tiangolo.com/) is a modern, fast
(high-performance), web framework for building HTTP APIs based on
standard Python type hints.

Example (*main.py*):

```python
from typing import Optional

from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: Optional[str] = None):
    return {"item_id": item_id, "q": q}
```

Run it with `uvicorn main:app --reload` and then open your browser at
<http://127.0.0.1:8000/items/5?q=somequery>.
