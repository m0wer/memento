---
title: asyncio
date: 2021-09-03
author: m0wer
tags: [ 'python', 'concurrency' ]
---

[`asyncio`](https://docs.python.org/3/library/asyncio.html) is a library to
write concurrent code using the `async`/`await` syntax.

Basic example:

```python
"""Asyncio example."""

import asyncio
from typing import Dict


async def function(number: int) -> str:
    """Sleep 1 second and return the passed number as a string."""
    await asyncio.sleep(1)
    return str(number)


async def main() -> None:
    """Call function 100 times and save the outputs in a dictionary."""
    args = list(range(100))
    results = await asyncio.gather(*[function(n) for n in args])

    result: Dict[int, str] = dict(zip(args, results))
    print(result)


asyncio.run(main())
```

This code runs in approximately one second, instead of the expected 100 seconds
of its non concurrent version.
