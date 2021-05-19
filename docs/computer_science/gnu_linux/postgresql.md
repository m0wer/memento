---
title: PostgresSQL
date: 2020-03-16
tags: [ 'postgresql', 'sql' ]
---

# Usage

Use `psql`.

Queries ignore case, so if any column name has capital letters in it, escape
it with double quotes ("). To scape a string use single quotes (').

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
