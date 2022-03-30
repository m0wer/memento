---
title: JavaScript basics
date: 2022-03-24
author: m0wer
---

# JavaScript basics

## Basic types

### Array

#### Methods

* `.find()`: returns the first element in the provided array that satisfies
  the provided testing function. If no values satisfy the testing function,
  `undefined` is returned. E.g., `array1.find(element => element > 10)`.

### Dictionary

#### Tips

##### Iterate keys and values

```javascript
for (const [key, value] of Object.entries(object)) {
  console.log(key, value);
}
```

##### Map a dictionary to a dictionary

```javascript
Object.fromEntries(Object.entries(obj).map(([k, v]) => [k, v["someKey"]]));
```

### Enum

There is no `Enum` in JavaScript but you can use:

```javascript
Object.freeze({ Apple: 0, Banana: 1, Cherry: 2});
```

## Debugging

### Logging

#### Recursively log object

If you `console.log()` an object, only the first levels of it will be shown.
To recursively log the whole object, use:

```javascript
console.dir(yourObject, { depth: null });
```
