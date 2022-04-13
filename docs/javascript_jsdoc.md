---
title: JSDoc
date: 2022-04-13
author: m0wer
---

# JSDoc

## Usage

### @type

Reference: [Use JSDoc: @type](https://jsdoc.app/tags-type.html).

### @example

```javascript
/**
 * Solves equations of the form a * x = b
 * @example
 * // returns 2
 * globalNS.method1(5, 10);
 * @example
 * // returns 3
 * globalNS.method(5, 15);
 * @returns {Number} Returns the value of x for the equation.
 */
globalNS.method1 = function (a, b) {
    return b / a;
};
```
