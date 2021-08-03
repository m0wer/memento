---
title: pytest
date: 2021-08-03
author: m0wer
tags: [ 'test', 'python' ]
---

# Mocking

## monkeypatch

Sometimes tests need to invoke functionality which depends on global settings
or which invokes code which cannot be easily tested such as network access.
The [monkeypatch](https://docs.pytest.org/en/latest/how-to/monkeypatch.html)
fixture helps you to safely set/delete an attribute, dictionary item or
environment variable, or to modify sys.path for importing.

You need to add `monkeypatch` as an argument to the test functions.

### Environment variables

```python
monkeypatch.setenv(name, value, prepend=None)
```
