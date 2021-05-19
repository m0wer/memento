---
title: PostgresSQL
date: 2020-03-16
tags: [ 'postgresql', 'sql' ]
---

# Usage

## psql

## Get column names of a table

```psql
SELECT column_name FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = '{table_name}';
```
Or, to get the column names along with their type use:

```psql
\d+ {table_name}
```
## Delete a table

```psql
DROP TABLE "{table_name}";
```

## Enable command timing

```pgsql
\timing [on|off]
```

* [stackoverflow](https://stackoverflow.com/questions/9063402/get-execution-time-of-postgresql-query/9064100)
