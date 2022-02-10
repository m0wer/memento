---
title: Jinja
date: 2021-04-24
author: m0wer
tags: [ 'jinja' ]
---

# Filters

Variables can be modified by filters. Filters are separated from the variable
by a pipe symbol (`|`) and may have optional arguments in parentheses.
Multiple filters can be chained. The output of one filter is applied to the
next.

## Built-in filters

These are some of
[built-in filters](https://jinja.palletsprojects.com/en/master/templates/#builtin-filters):

* `lower`: convert a value to lowercase.

# Loops

## For loop

### Accessing the parent Loop

The special loop variable always points to the innermost loop. If it’s desired
to have access to an outer loop it’s possible to alias it:

```jinja
<table>
{% for row in table %}
  <tr>
  {% set rowloop = loop %}
  {% for cell in row %}
    <td id="cell-{{ rowloop.index }}-{{ loop.index }}">{{ cell }}</td>
  {% endfor %}
  </tr>
{% endfor %}
</table>
```
