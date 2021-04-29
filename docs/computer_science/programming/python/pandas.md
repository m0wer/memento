---
title: Pandas
date: 2020-03-04
tags: [ 'pandas', 'python', 'data analysis' ]
---

# Usage

## Get data

### Read series from file

You can use

```python
series = pd.read_csv('csvfile.csv', header = None, index_col = 0, squeeze = True)
```

`squeeze` also works with `read_table`.


# Debug

## pandas.errors.DtypeWarning

Warning raised when reading different dtypes in a column from a file.

* [pandas.errors.DtypeWarning](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.errors.DtypeWarning.html)

# Reference

* [Nullable integer data
  type](https://pandas.pydata.org/pandas-docs/stable/user_guide/integer_na.html)
