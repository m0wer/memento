---
title: Python basics
date: 2021-04-09
author: m0wer
tags: [ 'python', 'programming' ]
---

# Python basics

## Built-in types

### Classes

A class is an object from which we can generate instances. A basic definition
of one is as follows

```python
class Whatever:
    def __init__(self,arg):
        self.arg = arg

    var = 3
     def function(self,n):
        ...
```

where `arg` is an argument that then becomes an attribute of the generated
instance, `var` is another attribute and `function` is a method of the class.

A more extensive definition can be found at
[python-docs](https://docs.python.org/3/tutorial/classes.html).

To get the class attributes of an object, do `object.__dict__`.

### Mapping Types (dict)

A mapping object maps hashable values to arbitrary objects. Mappings are
mutable objects. There is currently only one standard mapping type, the
dictionary.

#### setdefault

[`setdefault(key[, default])`](https://docs.python.org/3/library/stdtypes.html#dict.setdefault):
If `key` is in the dictionary, return its value. If not, insert key with a
value of `default` and return `default`. `default` defaults to `None`.

#### Rename a dictionary key

```python
mydict[k_new] = mydict.pop(k_old)
```

### Ranges

A `range` is a Python built-in type that represents an immutable sequence of
numbers and is commonly used for looping a specific number of times in
`for` loops. Some examples are

```python
for i in range(end):
    print(i)

for i in range(start,stop,step):
    print(i)
```

To reverse the order in the range you can do

```python
reversed(range(n))
```

### String

#### Methods

* `str.count(sub[, start[, end]])`: Return the number of non-overlapping
  occurrences of substring `sub` in the range [`start`, `end`].
* `str.removeprefix(prefix)`: If the string starts with the prefix string,
  return `str[len(prefix):]`. Otherwise, return a copy of the original string.
* `str.removesuffix(suffix)`: If the string ends with the suffix string and
  that suffix is not empty, return `str[:-len(suffix)]`. Otherwise, return a
  copy of the original string.
* `str.strip([chars])`: Return a copy of the string with the leading and
  trailing characters removed.


### Enum

Example:

```python
from enum import Enum

class Color(Enum):
  RED = 1
  GREEN = 2
  BLUE = 3
```

## Built-in functions

### enumerate

To iterate over a list keys and values use `enumerate()`. Example:

```python
some_list = ['a', 'b', 'c']
for index, value in enumerate(some_list):
  ...
```

### filter

Use
[`filter(function, iterable)`](https://docs.python.org/3/library/functions.html?highlight=filter#filter)
to construct an iterator from those elements of `iterable` for which `function`
returns true.

### getattr

```python
getattr(object, name[, default])
```

Return the value of the named attribute of `object`.`name` must be a string.
If the string is the name of one of the object's attributes, the result is the
value of that attribute. If the named attribute does not exist, `default` is
returned if provided, otherwise `AttributeError` is raised.

### isinstance

To check if an object is an instance of a class use
[`isinstance(object, class)`](https://docs.python.org/3/library/functions.html#isinstance).
For example:

```python
d = {"a": 4}

isinstance(d, dict)
```

### issubclass

[`issubclass(class, classinfo)`](https://docs.python.org/3/library/functions.html#issubclass):
Return `True` if `class` is a subclass (direct, indirect or virtual) of
`classinfo`. A class is considered a subclass of itself. `classinfo` may be a
tuple of class objects, in which case every entry in `classinfo` will be
checked. In any other case, a `TypeError` exception is raised.

### Sort

To sort the objects of a `list` based on an attribute of them you can do

```python
list.sort(key=lambda x: x.attribute, reverse=True) # Higher first
```

This fragment comes from
[stackoverflow](https://stackoverflow.com/questions/403421/how-to-sort-a-list-of-objects-based-on-an-attribute-of-the-objects).

## Other functions

### Shuffle

To shuffle the elements order inside a list you can do

```python
from random import shuffle
x = [i for i in range(10)]
shuffle(x)
```

This fragment comes from
[stackoverflow](https://stackoverflow.com/questions/976882/shuffling-a-list-of-objects).

## Generic Operating System Services

### os

#### listdir

[`os.listdir(path='.')`](https://docs.python.org/3/library/os.html#os.listdir)
returns a list containing the names of the entries in
the directory given by *path*.

## Text processing services

### re

The [`re`](https://docs.python.org/3/library/re.html) module provides regular
expression matching operations similar to those found in Perl.

#### Usage

##### Check if string matches a pattern

The usage is `re.match(pattern, string)`. Example:

```python
import re

string = "whatever"

if re.match("what.*", string):
  print("yes")
```

#### Tips

* Try your RegEx at [Pythex](https://pythex.org/).

### time

The module [`time`](https://docs.python.org/3/library/time.html?highlight=time#module-time)
provides various time-related functions.

### Usage

#### Measure elapsed time between two points

To measure elapsed time between two points do:

```python
import time

start = time.time()
print("hello")
end = time.time()
print(end - start)
```

## Data types

### datetime

#### Methods

* `timestamp()`: Return POSIX timestamp.
* `now()`: Return the current local date and time.

### enum

An enumeration is a set of symbolic names (members) bound to unique, constant
values. Within an enumeration, the members can be compared by identity, and
the enumeration itself can be iterated over.

Example:

```python
from enum import Enum

class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3

isinstance(Color.GREEN, Color) # True

color = Color.RED
color.name # RED
color.value # 1
```

Enumeration members are hashable, so they can be used in dictionaries and sets.

## I/O

### Files

You can operate with files from a filesystem directly from python. A common
way of doing so is

```python
f = open('[file]', '[mode]')
```

Where `[file]` is the file path and `[mode]` is one of the following modes:

* **w**: For rewritting the file.
* **r**: For reading from the file.
* **a**: For appending at the end of the file.

Then you can use the following methods (depending on the selected mode):

```python
f.write('test')
f.read()
...
```

Nevertheless, it is a good practice to use the `with` keyword when dealing with
file objects, since it will automatically close it after the work is done.
It can be used as follows

```python
with open('file_path') as f:
  file_data = f.read()
```

Otherwise, `f.close()` should be called in order to close the file and thus
freeing up any system resource used by it.

### String formatting

#### Formatted string literals (f-strings)

[Formatted string literals](https://docs.python.org/3/tutorial/inputoutput.html#formatted-string-literals)
(also called f-strings for short) let you include the value of Python
expressions inside a string by prefixing the string with `f` or `F` and writing
expressions as `{expression}`.

For example:

```python
name = "robot"
print(f"Hello {name}")
```

#### Scientific notation for numbers

To print a number using scientific notation with `n` decimals, do

```python
number = 0.000123
print("{:.{n}e}".format(number))
```

which will return `1.23e-04` with `n=2`.

#### Get the name of the weekday

To get the name of the weekday of a `datetime` object use `.strftime("%A")`.
For example:

```python
>>> from datetime import datetime as date
>>> date.today().strftime("%A")
'Monday'
```

## Internet protocols and support

### http.server

You can create a basic HTTP server that serves the files in the current
directory with

```bash
mkdir /tmp/www
echo "Hello world!" > /tmp/index.html
cd /tmp/www; python3 -m http.server
```

if you want to leave it running in the background even if you close the
console session, do `nohup python3 -m http.server &` instead.

## Built-in exceptions

Most common:

  * `TypeError`: Raised when an operation or function is applied to an object
    of inappropriate type.
  * `ValueError`: Raised when an operation or function receives an argument
    that has the right type but an inappropriate value.

### Custom exception

To provide more insightful error messages related to our code, we can create
custom exceptions. For example:

```python
class ColorError(ValueError):
    def __init__(self, color):
        message = f"Invalid color {color}."
        super().__init__(message)
```

## Functional programming modules

### functools

The [`functools`](https://docs.python.org/3/library/functools.html)
module is for higher-order functions: functions that act on or return
other functions.

#### Usage

##### Change function default argument value

```python
from functools import partial

def f(num: int = 0) -> str:
  return "The value of num is: " + str(num)

f_p = partial(f, num=1)

f_p()
```

To keep the docstring of the original function, just copy it with:

```python
f_p.__doc__ = f.__doc__
```

## Python runtime services

### Abstract Base Classes

This module provides the infrastructure for defining
[abstract base classes (ABCs)](https://docs.python.org/3/glossary.html#term-abstract-base-class)
in Python, as outlined in [PEP 3119](https://www.python.org/dev/peps/pep-3119).

To create an abstract base class, to define and interface and can be
inherited but not instantiated, do:

```python
from abc import ABC, abstractmethod

class Switchable(ABC):
    """Switchable interface."""
    is_on: bool = False

    @abstractmethod
    def turn_on(self):
    """Method to turn on.""

    @abstractmethod
    def turn_off(self):
    """Method to turn off.""

class LightBulb(Switchable):
    """Light bulb class."""
    def turn_on(self):
        self.is_on = True
        print("Light is on.")

    def turn_on(self):
        self.is_on = False
        print("Light is off.")

light_bulb_1 = LightBulb()

light_bulb_1.turn_on()
```

This code is an example for an abstract class that doesn't follow the
composition over inheritance principle. It would be better to implement
separate `turn_on` and `turn_off` functions that get a `Switchable` object
as their argument.

*Note*: Use `@abstractmethod` before `classmethod`. See
[Issue 16267](https://bugs.python.org/issue16267).

## Development tools

### typing

Provides runtime support for type hints.

#### Types

##### TypedDict

Special construct to add type hints to a dictionary. At runtime it is a plain
`dict`.

Example:

```python
class Point2D(TypedDict):
    x: int
    y: int
    label: str

a: Point2D = {'x': 1, 'y': 2, 'label': 'good'}  # OK
b: Point2D = {'z': 3, 'label': 'bad'}           # Fails type check
```

By default, all keys must be present in a `TypedDict`. It is possible to
override this by specifying totality. Usage:

```python
class point2D(TypedDict, total=False):
    x: int
    y: int
```
