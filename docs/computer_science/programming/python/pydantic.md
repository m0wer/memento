---
title: pydantic
date: 2021-08-16
author: m0wer
tags: [ 'data validation', 'typing' ]
---

[pydantic](https://pydantic-docs.helpmanual.io/): data validation and settings
management using python type annotations.

Enforces type hints at runtime, and provides user friendly errors when data is
invalid.

# Usage

The most basic example is:

```python
from datetime import datetime
from typing import List, Optional
from pydantic import BaseModel


class User(BaseModel):
    id: int
    name = 'John Doe'
    signup_ts: Optional[datetime] = None
    friends: List[int] = []


external_data = {
    'id': '123',
    'signup_ts': '2019-06-01 12:22',
    'friends': [1, 2, '3'],
}
user = User(**external_data)
print(user.id)
#> 123
print(repr(user.signup_ts))
#> datetime.datetime(2019, 6, 1, 12, 22)
print(user.friends)
#> [1, 2, 3]
print(user.dict())
"""
{
    'id': 123,
    'signup_ts': datetime.datetime(2019, 6, 1, 12, 22),
    'friends': [1, 2, 3],
    'name': 'John Doe',
}
"""
```

What's going on here:

* `id` is of type `int`; the annotation-only declaration tells `pydantic` that
  this field is required. Strings, bytes or floats will be coerced to ints if
  possible; otherwise an exception will be raised.
* `name` is inferred as a string from the provided default; because it has a
  default, it is not required.
* `signup_ts` is a `datetime` field which is not required (and takes the value
  `Nonei` if it's not supplied). `pydantic` will process either a unix
  timestamp int (e.g. 1496498400) or a string representing the date & time.
* `friends` uses python's typing system, and requires a list of integers.
  As with `id`, integer-like objects will be converted to integers.

If validation fails `pydantic` will raise an error with a breakdown of what
was wrong.

## Validators

Custom validation and complex relationships between objects can be achieved
using the `validator` decorator.

Example:

```python
from pydantic import BaseModel, ValidationError, validator


class UserModel(BaseModel):
    name: str
    username: str
    password1: str
    password2: str

    @validator('name')
    def name_must_contain_space(cls, v):
        if ' ' not in v:
            raise ValueError('must contain a space')
        return v.title()
```

The validation function will get the variable `name` value and can perform
checks or transformations to it. It should finally return the desired value
for the variable.
