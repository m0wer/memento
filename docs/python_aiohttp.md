---
title: AIOHTTP
date: 2022-04-10
author: m0wer
---

# AIOHTTP

## Usage

Basic example:

```python
import aiohttp
import asyncio

async def main():
    async with aiohttp.ClientSession() as session:
        async with session.get('http://httpbin.org/get') as resp:
            print(resp.status)
            print(await resp.text())

asyncio.run(main)
```

Other methods:

```python
session.put('http://httpbin.org/put', data=b'data')
session.delete('http://httpbin.org/delete')
session.head('http://httpbin.org/get')
session.options('http://httpbin.org/get')
session.patch('http://httpbin.org/patch', data=b'data')
```

### Headers

```python
headers = {
    'Accepts': 'application/json',
    'X-API_KEY': 'secret',
}

async with aiohttp.ClientSession(headers=headers) as session:
    ...
```
