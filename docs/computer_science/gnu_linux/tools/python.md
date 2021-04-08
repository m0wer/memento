---
title: Python Guide
date: 2017-10-10
tags: [ 'python3', 'programming', 'python', 'guide' ]
---

# Python Guide

## Usage

### Header

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""docstring"""

__version__ = "0.0.1a"
__author__ = "author"
__copyright__ = "Copyright"
__credits__ = ["author"]
__license__ = "GPL3"
__maintainer__ = "maintainer"
__email__ = "email"
__status__ = "Alpha"
```

### Classes

```python
class Whatever:
    def __init__(self,arg):
        self.arg = arg

    var = 3
     def function(self,n):
        ...
```

[python-docs](https://docs.python.org/3/tutorial/classes.html)

Get class attributes: `object.__dict__`

### Ranges

```python
for i in range(end):
    print(i)

for i in range(start,stop,step):
    print(i)
```

[pythoncentral](http://pythoncentral.io/pythons-range-function-explained/)

To reverse the order in the range:

```python
reversed(range(n))
```

### Sort

To sort a list of objects based on an attribute:

```python
list.sort(key=lambda x: x.attribute, reverse=True) # Higher first
```

[stackoverflow](https://stackoverflow.com/questions/403421/how-to-sort-a-list-of-objects-based-on-an-attribute-of-the-objects)

### Shuffle

To shuffle the elements order inside a list:

```python
from random import shuffle
x = [i for i in range(10)]
shuffle(x)
```

[stackoverflow](https://stackoverflow.com/questions/976882/shuffling-a-list-of-objects)

### Files I/O

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

## Debug

With `pdb`

```python
import pdb

pdb.set_trace()
 ```

[pythonconquerstheuniverse](https://pythonconquerstheuniverse.wordpress.com/2009/09/10/debugging-in-python/)

## Style (PEP-8)

### Indentation

4 spaces.

[pep-8](https://www.python.org/dev/peps/pep-0008/#indentation)

## Packages

### pprint

```python
import pprint

things = [a,b,c]

pprint.pprint(things)
```

[python-docs](https://docs.python.org/3/library/pprint.html)

## Tips

### Long strings and PEP8

Implicit concatenation might be the cleanest solution:

```python
s = "this is my really, really, really, really, really, really," \
    " really long string that I'd like to shorten."
```

[stackoverflow](https://stackoverflow.com/questions/1874592/how-to-write-very-long-string-that-conforms-with-pep8-and-prevent-e501)
