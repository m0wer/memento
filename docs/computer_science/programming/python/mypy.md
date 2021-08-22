---
title: mypy
date: 2021-08-17
author: m0wer
tags: [ 'typing', 'type check' ]
---

[`mypy`](https://mypy.readthedocs.io/en/stable/) is a static type checker for Python.

# Usage

## Pre-commit hook

To use `mypy` as a pre-commit hook, add:

```yaml
  - repo: 'https://github.com/pre-commit/mirrors-mypy'
    rev: ''
    hooks:
      - id: 'mypy'
        args: []
        additional_dependencies:
          - 'pydantic'
```

For extended support for [`pydantic`](pydantic.md) don't forget to add the
additional dependency and enable the plugin in `pyproject.toml` with:

```toml
# --------- mypy -------------

[tool.mypy]
plugins = ["pydantic.mypy"]
```

# Tips

## Ignore type checking in one line

To ignore type checking in one particular line of the code, add the comment
`# type: ignore` at the end of that line
