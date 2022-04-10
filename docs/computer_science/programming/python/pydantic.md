---
title: Pydantic
date: 2021-08-16
author: m0wer
tags: [ 'data validation', 'typing' ]
---

# Pydantic

[pydantic](https://pydantic-docs.helpmanual.io/): data validation and settings
management using python type annotations.

Enforces type hints at runtime, and provides user friendly errors when data is
invalid.

## Usage

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
##> 123
print(repr(user.signup_ts))
##> datetime.datetime(2019, 6, 1, 12, 22)
print(user.friends)
##> [1, 2, 3]
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

### Validators

Custom validation and complex relationships between objects can be achieved
using the `validator` decorator.

Example:

```python
from pydantic import BaseModel, validator


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

You can use validators to set the value of an attribute as a combination
of others if undefined:

```python
from typing import Optional

from pydantic import BaseModel, validator


class UserModel(BaseModel):
    name: str
    password1: str
    password2: str
    username: Optional[str] = None
    accepted_tos: bool = False

    @validator('username', pre=True, always=True)
    def default_username(cls, v, values):
        if v is None:
            v = values['name']
        return v
```

`always=True` is required in this example since otherwise when `username` is
not passed, the validator won't be executed. `pre=True` makes it run before
any other validator so that `username` is defined in before other possible
validations.

Note that `values` only contains the class attributes defined *before* the
one that is being validated. In the example above, `values` in the
`default_username` validator won't contain the `accepted_tos` key.

#### Root validators

Validation can also be performed on the entire model's data.

You can decorate a function with `@root_validator` and it will get all of the
values as an argument. This function should process them and raise an exception
or return the desired values dictionary.

For example:

```python
@root_validator
def check_passwords_match(cls, values):
    pw1, pw2 = values.get('password1'), values.get('password2')
    if pw1 is not None and pw2 is not None and pw1 != pw2:
        raise ValueError('passwords do not match')
    return values
```

`root_validator` takes `pre` as argument but not `always`, since its executed
always anyways.

*Note*: there is a bug
([#1895](https://github.com/samuelcolvin/pydantic/issues/1895))
that prevents subclasses to override the `root_validator` method defined in
the parent class. A workaround for `BaseModel` subclasses is described in the
issue comments but not for pydantic dataclasses. In this second case, a
solution is to not define the root validator in the parent class and do it
only on the child.

### Exporting

Options:

* `model.json(exclude_none=True)`
* `model.dict(exclude_none=True)`

### Types

* `pydantic.HttpUrl`
* `pydantic.color.Color`
