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

## Sort

To sort the objects of a `list` based on an attribute of them you can do

```python
list.sort(key=lambda x: x.attribute, reverse=True) # Higher first
```

This fragment comes from
[stackoverflow](https://stackoverflow.com/questions/403421/how-to-sort-a-list-of-objects-based-on-an-attribute-of-the-objects).

# Other fucntions

## Shuffle

To shuffle the elements order inside a list you can do

```python
from random import shuffle
x = [i for i in range(10)]
shuffle(x)
```

This fragment comes from
[stackoverflow](https://stackoverflow.com/questions/976882/shuffling-a-list-of-objects).

# Files I/O

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
