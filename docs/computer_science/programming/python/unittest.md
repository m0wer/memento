---
title: unittest
date: 2021-08-23
author: m0wer
tags: [ 'test' ]
---

The [`unittest`](https://docs.python.org/3/library/unittest.html) unit
testing framework was originally inspired by JUnit and has a similar flavor as
major unit testing frameworks in other languages. It supports test automation,
sharing of setup and shutdown code for tests, aggregation of tests into
collections, and independence of the tests from the reporting framework.

# Mock

[`unittest.mock`](https://docs.python.org/3/library/unittest.mock.html) is a
library for testing in Python. It allows you to replace parts of your system
under test with mock objects and make assertions about how they have been used.

## Usage

First, `from unittest.mock import patch`. Then set the appropriate
decorator for the function and expect a new argument related to the mock
object. This object will have methods such as:

* `assert_called`: assert that the mock was called at least once.
* `assert_called_once`: assert that the mock was called exactly once.
* `assert_called_with`: asserts that the last call has been made in a
  particular way.
* `assert_called_once_with`: assert that the mock was called exactly once
  and that call was with the specified arguments.

And attributes such as:

* `call_args`: either `None` (if the mock hasn't been called), or the
  arguments that the mock was last called with.

### Function

Use `@patch("{{function}}", {{return_value}})`.

### Class Method

Use `@patch.object({{class}}, {{method}}, return_value={{return_value}})`.

For example:

```python
@patch.object(SomeClass, 'class_method')
def test(mock_method):
    SomeClass.class_method(3)
    mock_method.assert_called_with(3)

test()
```

### Abstract class

To patch an abstract class to be able to instantiate it, without having to
create a fake class that inherits from it, you can patch it as follows:

```python
@patch.object(MyAbcClass, '__abstractmethods__', set())
```

or if you want to patch some attributes and/or methods at the same time:

```python
@patch.multiple(MyAbcClass, __abstractmethods__=set())
```
