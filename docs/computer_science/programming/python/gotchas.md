---
title: Python gotchas
date: 2021-04-11
author: m0wer
tags: [ 'python' ]
---

# Two dimensional array initialization

Imagine we want to initialize an array containing a few empty arrays inside,
something like

```python
arr = [[], [], []]
```

If we want to save time and/or keystrokes, we might be tempted to do it as
follows

```python
arr = [[]] * 3
```

```python
>>> arr
[[], [], []]
```

Which looks like what we wanted right? Well it does, but the gotcha is that
all of the inner arrays are actually the same object copied so if you modify
one of them, "all of them" will be equally affected. For example,

```python
>>> arr[0].append('test')
>>> arr
[['test'], ['test'], ['test']]
```

So what you should do instead is:

```python
arr = [[] for _ in range(3)]
```
