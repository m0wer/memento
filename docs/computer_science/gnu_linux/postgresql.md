---
title: PostgreSQL
date: 2020-03-16
tags: [ 'postgresql', 'sql' ]
---

# Usage

Use `psql`.

Queries ignore case, so if any column name has capital letters in it, escape
it with double quotes ("). To scape a string use single quotes (').

To select the database to work in do

```psql
\connect {database_name}
```

or `\c {database_name}` in short.

## Basic operations

### Delete a table

```psql
DROP TABLE "{table_name}";
```

### GROUP BY

Reference:
[PostgreSQL GROUP BY](https://www.postgresqltutorial.com/postgresql-group-by/)

### UPDATE

To update the values of some columns, use
[UPDATE](https://www.postgresql.org/docs/9.1/sql-update.html).

The general basic syntax is as follows:

```psql
UPDATE table_name
SET column1 = value1,
    column2 = value2,
    ...
WHERE condition;
```

## Query operators

### NULLIF

The [`NULLIF(value1, value2)`](https://www.postgresql.org/docs/current/functions-conditional.html#FUNCTIONS-NULLIF)
function returns a null value if `value1` equals `value2`; otherwise it returns
`value1`.

It can be useful for avoiding divisions by 0 (e.g. set `value2` to 0).

## Time stamp operations

### Get only part of the time stamp

To get only a part of the time stamp (e.g., day, hour...) or to get it in
another format (e.g., epoch), use `date_part()`. For example, to get the
hour of a `timestamp` do:

```psql
date_part('hour', timestamp '2001-02-16 20:38:40')
```

which will return `20`. The second argument of the function can be the name of
a column.

## Meta

### Get column names of a table

```psql
SELECT column_name FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = '{table_name}';
```
Or, to get the column names along with their type use:

```psql
\d+ {table_name}
```

### Enable command timing

```pgsql
\timing [on|off]
```

* [stackoverflow](https://stackoverflow.com/questions/9063402/get-execution-time-of-postgresql-query/9064100)

### Stop/kill process

First locate the process `pid` with

```psql
SELECT pid, query FROM pg_stat_activity WHERE state = 'active';
```

Then, stop or kill the process with SELECT `pg_cancel_backend({pid})` or
`pg_termiante_backend({pid})` respectively.

## Configuration

You can use [PGTune](https://pgtune.leopard.in.ua/#/) to calculate
configuration for PostgreSQL based on the maximum performance for a given
hardware configuration.

### Parallelization

To tune the number of workers edit `postgresql.conf` and in the
*- Asynchronous Behavior -* section edit `max_worker_processes`,
`max_parallel_workers_per_gather` and `max_parallel_workers`.
