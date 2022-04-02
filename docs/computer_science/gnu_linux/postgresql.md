---
title: PostgreSQL
date: 2020-03-16
tags: [ 'postgresql', 'sql' ]
---

# PostgreSQL

## Usage

Use `psql`.

Queries ignore case, so if any column name has capital letters in it, escape
it with double quotes ("). To scape a string use single quotes (').

To select the database to work in do

```psql
\connect {database_name}
```

or `\c {database_name}` in short.

### Basic operations

#### Delete a table

```psql
DROP TABLE "{table_name}";
```

#### Add a new column

To add a new column, use
[`ALTER TABLE`](https://www.postgresql.org/docs/current/sql-altertable.html).

For example:

```psql
ALTER TABLE {table_name}
  ADD IF NOT EXISTS {column_name} {data_type}
```

#### GROUP BY

Reference:
[PostgreSQL GROUP BY](https://www.postgresqltutorial.com/postgresql-group-by/)

#### UPDATE

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

##### From subquery

The most efficient way appears to be the following.

```psql
UPDATE {table}
SET {column1}=subquery.{column1},
    {column2}=subquery.{column2}
FROM ({subquery}) AS subquery
WHERE {table}.{id} = subquery.{id};
```

Other options are to perform a `JOIN` but the syntax is less clear and the
performance seems to be worse.

#### Window functions

Window functions allow to perform the calculation across a set of rows related
to the current row.

The simplified syntax is:

```psql
window_function(arg1, arg2,..) OVER (
   [PARTITION BY partition_expression]
   [ORDER BY sort_expression [ASC | DESC] [NULLS {FIRST | LAST }])
```

So for example a moving average of the last 28 days could be obtained with:

```psql
SELECT
    AVG({column})
        OVER (
         ORDER BY {date_column}
               RANGE BETWEEN '28 day' PRECEDING AND current row)
         AS rolling_average
 FROM
     {table}
```

### Query operators

#### NULLIF

The [`NULLIF(value1, value2)`](https://www.postgresql.org/docs/current/functions-conditional.html#FUNCTIONS-NULLIF)
function returns a null value if `value1` equals `value2`; otherwise it returns
`value1`.

It can be useful for avoiding divisions by 0 (e.g. set `value2` to 0).

### String functions and operators

Reference: [PostgreSQL Documentation](https://www.postgresql.org/docs/current/functions-string.html)


#### concat_ws

To concatenate strings with a separator, use
`concat_ws({separator}, {val1}, {...})`.

For example: `concat_ws(',', 'abcde', 2, NULL, 22) → abcde,2,22`.

#### COUNT

##### Count NULL values

```psql
SELECT COUNT(*) FROM table WHERE column IS NULL;
```
`COUNT` only conseiders non null values so use `COUNT(*)` (which counts the
row) instead of `COUNT(column)` because the later would always return 0 since
the filter gets only the null values of `column`.

### Time stamp operations

#### Get only part of the time stamp

To get only a part of the time stamp (e.g., day, hour...) or to get it in
another format (e.g., epoch), use `date_part()`. For example, to get the
hour of a `timestamp` do:

```psql
date_part('hour', timestamp '2001-02-16 20:38:40')
```

which will return `20`. The second argument of the function can be the name of
a column.

If instead you want to truncate a timestamp to a specified level of precission,
use `date_trunc('datepart', field)`.

### Constraints

#### Check that a string is a valid timezone

Use the constraint `CHECK (now() AT TIME ZONE timezone IS NOT NULL)`. For
example:

```psql
CREATE TABLE locations (
    location_id SERIAL PRIMARY KEY,
    name TEXT,
    timezone TEXT NOT NULL CHECK (now() AT TIME ZONE timezone IS NOT NULL)
);
```

### Meta

#### Get column names of a table

```psql
SELECT column_name FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = '{table_name}';
```
Or, to get the column names along with their type use:

```psql
\d+ {table_name}
```

#### Enable command timing

```pgsql
\timing [on|off]
```

* [stackoverflow](https://stackoverflow.com/questions/9063402/get-execution-time-of-postgresql-query/9064100)

#### Stop/kill process

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

## Administration

### Change user password

```sql
ALTER USER user_name WITH PASSWORD 'new_password';
```

## Tips

### Copy data manually between different databases

If you want to copy just a few rows between tables in different databases and
even slightly different schema, you can use the following commands:

```psql
COPY (SELECT * FROM user WHERE id = 42) TO STDOUT WITH (FORMAT CSV, HEADER);
```

Which returns:

```csv
id,name,created_at,updated_at
42,Some User,2022-03-01 06:18:53.37+00,2022-03-01 06:18:53.37+00
```

Then, in the other database:

```psql
COPY user FROM STDIN WITH (FORMAT CSV, HEADER);
```
Paste the result from the first query and press `Ctrl+D`.

## Stop remote connections

Some operations, like dropping a database, require that the database has no connections. To stop all remote connections and prevent them from connecting again, do:

```psql
ALTER DATABASE somedatabase ALLOW_CONNECTIONS = OFF;

SELECT pg_terminate_backend(pid)
FROM pg_stat_activity
WHERE datname = 'somedatabase';
```

But if you are using PostgreSQL 13 or above, for dropping a table you can directly do:

```psql
DROP DATABASE db_name WITH (FORCE);
```

## Performance optimization

### Get the 20 slowest queries

```psql
SELECT substring(query, 1, 50) AS short_query,
              round(total_time::numeric, 2) AS total_time,
              calls,
              round(mean_time::numeric, 2) AS mean,
              round((100 * total_time / sum(total_time::numeric) OVER ())::numeric, 2) AS percentage_cpu
FROM  pg_stat_statements
ORDER BY total_time DESC
LIMIT 20;
```

## Reference

### Data types

* [Numeric Types](https://www.postgresql.org/docs/current/datatype-numeric.html)
