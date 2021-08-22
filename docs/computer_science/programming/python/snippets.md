---
title: Python snippets
date: 2021-04-09
author: m0wer
tags: [ 'python', 'programming' ]
---

# Header

This header should go on top of python scripts.

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""docstring"""

__version__ = "0.0.1a"
__author__ = "author"
__copyright__ = "Copyright"
__credits__ = ["author"]
__license__ = "GPL3"
__maintainer__ = "maintainer"
__email__ = "email"
__status__ = "Alpha"
```

# Basic operations

## Find first element  in dictionary that satisfies a condition

```python
next(item for item in {dict} if {{ condition }})
```

# I/O

## Create a directory if it doesn't exist

```python
import os

dir_path = '{dir_path}'
if not os.path.exists(dir_path):
    os.makedirs(dir_path)
```

# Network

## Download a file

To download a file from a URL do:

```python
import urllib.request
urllib.request.urlretrieve('{url}', '{destination_path}')
```
