---
title: statsmodels
date: 2021-08-11
author: m0wer
tags: [ 'statistics', 'linear regression' ]
---

[`statsmodels`](https://www.statsmodels.org/) is a Python module that provides
classes and functions for the estimation of many different statistical models,
as well as for conducting statistical tests, and statistical data exploration.

# Usage

## Linear regression

Using Ordinary Least Squares.


```python
import statsmodels.api as sm
Y = [1, 2]
X = [0, 1]
X = sm.add_constant(X)
model = sm.OLS(Y,X)
results = model.fit()
results.summary()
```

As expected the resulting coefficients are 1 for the constant and 1 for $X$:

\[
Y = 1 + X
\]
