---
title: Python logging
date: 2022-04-08
author: m0wer
---

# Python logging

Basic configuration:

```python
import logging

logging.basicConfig(
    format='%(asctime)s %(levelname)s %(message)s',
    level=logging.INFO,
    datefmt='%Y-%m-%d %H:%M:%S'
)

logging.info('Just a random string...')
# 2030-01-01 00:00:00 INFO Just a random string...
```
