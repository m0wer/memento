---
title: psycopg2
date: 2021-08-04
author: m0wer
tags: [ 'postgresql' ]
---

# Usage

## Dynamic SQL generation

To replace parts of an SQL query with variables, there are three main ways of
doing it:

  * SQL query string formatting
    (e.g., `"SELECT * FROM table WHERE id = {id}".format(id=42)`): **DON'T**.
    This can potentially lead to SQL injections.
  * `cursor.execute` `vars`: Use this option when replacing values that aren't
    column names or similar. For example:
    ```python
    cur.execute("insert into table values (%s, %s)", [10, 20])
    ```
  * `psycopg2.sql`: this module will allow you to generate SQL statements on
    the fly, separating clearly the changing parts of the statement from the
    query parameters. Example:
    ```python
    from psycopg2 import sql

    cur.execute(
        sql.SQL("insert into {} values (%s, %s)")
            .format(sql.Identifier('table')),
        [10, 20])
    ```

    If part of your query is a variable sequence of arguments, such as a
    comma-separated list of field names, you can use the `SQL.join()` method to
    pass them to the query:

    ```python
    query = sql.SQL("select {fields} from {table}").format(
      fields=sql.SQL(',').join([
          sql.Identifier('field1'),
          sql.Identifier('field2'),
          sql.Identifier('field3'),
      ]),
      table=sql.Identifier('some_table'))
    ```
