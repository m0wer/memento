---
title: Database Normalization
date: 2022-01-18
author: m0wer
---

Database normalization is the process of structuring a database, usually a
relational database, in accordance with a series of so-called normal forms in
order to reduce data redundancy and improve data integrity.

# Normal forms

*Note: Primary Keys in bold.*

## UNF

* Unique PK.

## 1NF

* Each column of a table must have a single value. Are you repeatedly inserting
  the same values for a set of columns?


### Example

Convert this:

| Customer | Customer phone | Product | Price |
|----------|----------------|---------|-------|
| Bob      | 00000000       | apple   | 1     |
| Alice    | 11111111       | orange  | 2     |
| Bob      | 00000000       | orange  | 2     |

To this:

| **Product ID** | Name   | Price |
|----------------|--------|-------|
| 1              | apple  | 1     |
| 2              | orange | 2     |

| **Customer ID** | Name   | Phone |
|-----------------|--------|-------|
| 1               | Bob    | 1     |
| 2               | Alice  | 2     |


## 2NF

*

