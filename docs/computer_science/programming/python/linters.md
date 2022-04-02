---
title: Linters
date: 2021-09-07
author: m0wer
---

# Pydocstyle

[PyCQA/pydocstyle](https://github.com/PyCQA/pydocstyle) is a static analysis
tool for checking compliance with Python docstring conventions.

## Tips

### Allow missing docstrings when overriding methods

To allow missing docstrings when overriding methods you can use the
[`@overrides`](python_decorators.md#overrides) decorator and the command line option
`--ignore-decorator=overrides` or the setting `ignore_decorator = "overrides"`
in the configuration file.
