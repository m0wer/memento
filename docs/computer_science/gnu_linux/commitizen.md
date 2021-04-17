---
title: Commitizen
date: 2021-04-17
author: m0wer
tags: [ 'git' ]
---

[Commitizen](https://commitizen-tools.github.io/commitizen/) is a tool that
defines a standard way of committing.

It can bump the version of your project automatically based on commits and
generate a changelog file.

# Installation

```bash
pip install commitizen
```

# Configuration

If your project version is not detected automatically or it isn't specified you
can add the files where the version appears or the version respectively to
`.cz.toml` as shown in the following examples:

```toml
[tool.commitizen]
version_files = [
    "src/__version__.py",
    "setup.py",
]
```

```toml
[tool.commitizen]
version = "0.2.2"
```

# Usage

To commit:

```bash
cz commit
```

To bump the version and update the changelog:

```bash
cz bump --changelog --no-verify
```
