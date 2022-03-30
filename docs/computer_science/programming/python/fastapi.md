---
title: FastAPI
date: 2021-08-11
author: m0wer
tags: [ 'api', 'http' ]
---

# FastAPI

[FastAPI](https://fastapi.tiangolo.com/) is a modern, fast
(high-performance), web framework for building HTTP APIs based on
standard Python type hints.

Example (*main.py*):

```python
from typing import Optional

from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: Optional[str] = None):
    return {"item_id": item_id, "q": q}
```

Run it with `uvicorn main:app --reload` and then open your browser at
<http://127.0.0.1:8000/items/5?q=somequery>.

## Usage

There are two main ways of using this module, with the decorator
`@app.get("{{route}}")` or with
`FastAPI().add_route("{{route}}", {{function}})`.

The first alternative is by far the most common, but if you want to separate
the functions from the HTTP API entrypoint, you have to use the second option.
For example:

```
from fastapi import FastAPI

api = FastAPI()

def hello(name: str) -> str:
  return "Hello " + name + "!"

api.add_route('/hello', hello)
```

The advantage of this alternative is that we can import the function
from another module.

If you need to change the default value of some argument of the original
function, you can use [`functools`](basics.md#functools). This might be necessary
if an argument is a list, since you'll need to set its default value
to `Query()` you can change it with `functools` instead of modifying
the original function (which would be pretty ugly). Make sure of copying
the original docstring.

Nevertheless, this approach has some caveats such as not handling exceptions
raised from the imported function. The best solution for this appears to be
defining a wrapper function that handles the arguments, calls the imported
function or method and handles the exceptions raising the proper
`HTTPException`.

### Dependency injection

A FastAPI decorated function can import the necessary arguments for other
functions or objects.

For example:

```python
from typing import Optional

from fastapi import Depends, FastAPI

app = FastAPI()


async def common_parameters(q: Optional[str] = None, skip: int = 0, limit: int = 100):
    return {"q": q, "skip": skip, "limit": limit}


@app.get("/items/")
async def read_items(commons: dict = Depends(common_parameters)):
    return commons
```

In this example, the function `read_items` will get the parameters
for the function `common_parameters` (i.e., `q`, `skip`, `limit`) allowing the
optional ones to be set or not. Then, the passed parameters will be passed
as a dictionary as the `commons` argument value of `read_itmes`. This is
thanks to `Depends`.

`Depends` can also be used with classes, and we could get an instance of a
class directly to our function. For example by setting the argument:
`car: Car = Depends(Car)` or `car: Car = Depends()` (which assumes that it
depends on the class defined in the type hint).

## JSON encoder

The default the responses will be serialized to JSON. You can use a different
JSON encoder than the default one, for example
[ijl/orjson](https://github.com/ijl/orjson) which is more efficient and
natively support serialization of dataclasses and more.

To set the default encoder do:

```python
from fastapi import FastAPI
from fastapi.responses import ORJSONResponse

FastAPI(default_response_class=ORJSONResponse)
```

## Testing

### Testing startup and shutdown events

When you need your event handlers (`startup` and `shutdown`) to run in your
tests, you can use the `TestClient` with a with statement:

```python
import pytest
from fastapi.testclient import TestClient
from api.main import api

@pytest.fixture
def client():
    with TestClient(api) as client:
        yield client

def test_endpoint(client):
    response = client.get("/endpoint")

    assert response.status_code == 200
```

## Performance

Performance can be hugely improved with some minor changes:

* Use `orjson` (faster JSON serialization):

  ```python
  from fastapi import FastAPI
  from fastapi.responses import ORJSONResponse
  app = FastAPI(default_response_class=ORJSONResponse)
  ...
  ```
* When using `response_model=...`, directly return a `Response` object if
  you've already done the `pydantic` model validation
  (or if you don't want to validate the object at all). Otherwise the
  validation will happen twice which is computationally expensive.

  ```python
  ...
  from fastapi.encoders import jsonable_encoder

  class Thing(BaseModel):
    name: str

  @app.get("/thing', response_model=Thing)
  def get_thing():
      thing: Thing = Thing(name="something")
      return ORJSONResponse(content=jsonable_encoder(result))
  ```
* Use [long2ice/fastapi-cache](https://github.com/long2ice/fastapi-cache)
  to cache responses and set the appropriate `ETag` and `Cache-Control`
  headers.

  You will need to use the `PickleCoder` coder if you want to cache responses
  directly. Otherwise if you directly return a `dict` or similar (not a
  `Response`) the cache will store that object and then the model validation
  will be executed unnecessarily every time the endpoint is called..


All together:

```python
from fastapi import FastAPI
from fastapi.responses import ORJSONResponse
from fastapi.encoders import jsonable_encoder
from fastapi_cache.backends.inmemory import InMemoryBackend
from fastapi_cache.coder import PickleCoder

app = FastAPI(default_response_class=ORJSONResponse)

@app.on_event("startup")
async def startup():
    FastAPICache.init(InMemoryBackend())

class Thing(BaseModel):
  name: str

@app.get("/thing', response_model=Thing)
@cache(expire=7 * 24 * 60 * 60, coder=PickleCoder)  # 7 days
def get_thing():
    thing: Thing = Thing(name="something")
    return ORJSONResponse(content=jsonable_encoder(result))
```

## Logging

To add custom log messages to the `uvicorn` output, the dirty way, get the
logger called `uvicorn`:

```python
logger = logging.getLogger("uvicorn")
```
