---
title: requests
date: 2021-08-17
author: m0wer
tags: [ 'http' ]
---

[Requests](https://docs.python-requests.org/en/master/) is an elegant and
simple HTTP library for Python, built for human beings.

# Usage

## Make a request

```python
import requests
r = requests.get('https://api.github.com/events')
r.text
r.json()
```
