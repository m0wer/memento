---
title: tenacity
date: 2021-11-17
author: m0wer
---

[jd/tenacity](https://github.com/jd/tenacity) is a retrying library for Python.

# Usage

## Try a maximum of n times with exponential wait time between attempts

```python
from tenacity import retry, stop_after_attempt, wait_exponential

@retry(stop=stop_after_attempt(3), wait=wait_exponential(multiplier=0.1))
def somefunction():
  raise Exception
```

The function will be retried a maximum of 3 times, waiting 0.1 s, 0.2 s and 0.4
s between each attempt respectively.

## Catch only some kind of errors

Use `@retry(retry=retry_if_exception_type(IOError))`.

Several types of exceptions can be combined as follows:

```python
@retry(retry=(retry_if_exception_type(IOError) | retry_if_exception_type(TimeoutError)))
```
