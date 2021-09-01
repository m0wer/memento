---
title: asyncpg
date: 2021-09-01
author: m0wer
tags: [ 'postgresql' ]
---

[MagicStack/asyncpg](https://github.com/MagicStack/asyncpg) is a fast
PostgreSQL Database Client Library for Python/asyncio.

Basic usage:

```python
import asyncio
import asyncpg

async def run():
    conn = await asyncpg.connect(user='user', password='password',
                                 database='database', host='127.0.0.1')
    values = await conn.fetch(
        'SELECT * FROM mytable WHERE id = $1',
        10,
    )
    await conn.close()

loop = asyncio.get_event_loop()
loop.run_until_complete(run())
```
