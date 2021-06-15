---
title: Python basics
date: 2021-04-09
author: m0wer
tags: [ 'python', 'programming' ]
---

# Built-in types

## Classes

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

## Ranges

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

# Built-in functions

## isinstance

To check if an object is an instance of a class use
[`isinstance(object, class)`](https://docs.python.org/2/library/functions.html#isinstance).
For example:

```python
d = {"a": 4}

isinstance(d, dict)
```

## Sort

To sort the objects of a `list` based on an attribute of them you can do

```python
list.sort(key=lambda x: x.attribute, reverse=True) # Higher first
```

This fragment comes from
[stackoverflow](https://stackoverflow.com/questions/403421/how-to-sort-a-list-of-objects-based-on-an-attribute-of-the-objects).

# Other functions

## Shuffle

To shuffle the elements order inside a list you can do

```python
from random import shuffle
x = [i for i in range(10)]
shuffle(x)
```

This fragment comes from
[stackoverflow](https://stackoverflow.com/questions/976882/shuffling-a-list-of-objects).

# Generic Operating System Services

## os

### listdir

[`os.listdir(path='.')`](https://docs.python.org/3/library/os.html#os.listdir)
returns a list containing the names of the entries in
the directory given by *path*.

# Text processing services

## re

The [`re`](https://docs.python.org/3/library/re.html) module provides regular
expression matching operations similar to those found in Perl.

### Usage

#### Check if string matches a pattern

The usage is `re.match(pattern, string)`. Example:

```python
import re

string = "whatever"

if re.match("what.*", string):
  print("yes")
```

### Tips

* Try your RegEx at [Pythex](https://pythex.org/).

## time

The module [`time`](https://docs.python.org/3/library/time.html?highlight=time#module-time)
provides various time-related functions.

## Usage

### Measure elapsed time between two points

To measure elapsed time between two points do:

```python
import time

start = time.time()
print("hello")
end = time.time()
print(end - start)
```

# I/O

## Files

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

## String formatting

### Scientific notation for numbers

To print a number using scientific notation with `n` decimals, do

```python
number = 0.000123
print("{:.{n}e}".format(number))
```

which will return `1.23e-04` with `n=2`.

### Get the name of the weekday

To get the name of the weekday of a `datetime` object use `.strftime("%A")`.
For example:

```python
>>> from datetime import datetime as date
>>> date.today().strftime("%A")
'Monday'
```

# Internet protocols and support

## http.server

You can create a basic HTTP server that serves the files in the current
directory with

```bash
mkdir /tmp/www
echo "Hello world!" > /tmp/index.html
cd /tmp/www; python3 -m http.server
```

if you want to leave it running in the background even if you close the
console session, do `nohup python3 -m http.server &` instead.
