---
title: pytest
date: 2021-08-03
author: m0wer
tags: [ 'test', 'python' ]
---

# Usage

Invoke with `python -m pytest` so that the current directory is included
to the python path.

## Execute just one test or test class

```python
pytest test_server.py::TestClass::test_method
```

or


```python
pytest test_server.py::TestClass
```

# Reference

## Parametrization

To run the same test several times with different variables use
`@pytest.mark.parametrize()`.

```python
import pytest


@pytest.mark.parametrize("test_input,expected", [("3+5", 8), ("2+4", 6), ("6*9", 42)])
def test_eval(test_input, expected):
    assert eval(test_input) == expected
```

## Mocking

### monkeypatch

Sometimes tests need to invoke functionality which depends on global settings
or which invokes code which cannot be easily tested such as network access.
The [monkeypatch](https://docs.pytest.org/en/latest/how-to/monkeypatch.html)
fixture helps you to safely set/delete an attribute, dictionary item or
environment variable, or to modify sys.path for importing.

You need to add `monkeypatch` as an argument to the test functions.

#### Environment variables

```python
monkeypatch.setenv(name, value, prepend=None)
```
