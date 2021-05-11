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

## DataFrame

### Methods

#### to_sql

[pandas.DataFrame.to_sql](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_sql.html)(name, con, schema=None, if_exists='fail', index=True, index_label=None, chunksize=None, dtype=None, method=None) writes records stored in a DataFrame to a SQL database.

Example:

```python
import pandas as pd
from sqlalchemy import create_engine

engine = create_engine('sqlite://', echo=False)
df = pd.DataFrame({'name' : ['User 1', 'User 2', 'User 3']})
df.to_sql('users', con=engine)
```

This will create a new table called `users` and fill it with the `DataFrame`.
If the table already exists, it will fail. Set `if_exists='append'` or
`if_exists='replace'` for other behaviors.

# Debug

## pandas.errors.DtypeWarning

Warning raised when reading different dtypes in a column from a file.

* [pandas.errors.DtypeWarning](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.errors.DtypeWarning.html)

# Reference

* [Nullable integer data
  type](https://pandas.pydata.org/pandas-docs/stable/user_guide/integer_na.html)
