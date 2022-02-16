---
title: Database Normalization
date: 2022-01-18
author: m0wer
---

Database normalization is the process of structuring a database, usually a
relational database, in accordance with a series of so-called normal forms in
order to reduce data redundancy and improve data integrity.

# Definitions

* **Candidate key (CK)**: any set of columns that have a unique combination of
  values in each row satisfying that removing any column would possibly
  produce duplicate rows.
* **Primary key (PK)**: specific choice of a minimal set of attributes
  (columns) that uniquely specify a tuple (row). "Which attributes identify a
  record."

# Normal forms

*Note: Primary Keys in bold.*

## UNF

* Unique PK.

## 1NF

Each column of a table must have a single value.

### Example

Convert this:

| Customer | Customer phone | Product           |
|----------|----------------|-------------------|
| Bob      | 00000000       | [apple, orange]   |
| Alice    | 11111111       | orange            |

Into this:

| Customer | Customer phone | Product |
|----------|----------------|---------|
| Bob      | 00000000       | apple   |
| Alice    | 11111111       | orange  |
| Bob      | 00000000       | orange  |

## 2NF

Each column value should only depend on the candidate key.

### Example

Convert this:

| **Product name** | Box weight | Quality | Price |
|------------------|------------|---------|-------|
| Apple            | 1 kg       | 1       | 2     |
| Apple            | 1 kg       | 2       | 1.5   |
| Orange           | 5 kg       | 1       | 4     |
| Orange           | 5 kg       | 2       | 2     |

To this:

| **Product name** | Box weight |
|------------------|------------|
| Apple            | 1 kg       |
| Orange           | 5 kg       |

| **Product name** | **Quality** | Price |
|------------------|-------------|-------|
| Apple            | 1           | 2     |
| Apple            | 2           | 1.5   |
| Orange           | 1           | 4     |
| Orange           | 2           | 2     |

In the original table, the `Box weight` depended only on the candidate key
`Product name`, but the price depended also on the quality. That's why it
should be separated into two tables to avoid duplication.

## 3NF

There should be no transitive functional dependencies. If a column can be
determined from another (functional dependency) the dependent column should
be in another table.

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

| **Customer ID** | **Product ID** |
|-----------------|----------------|
| 1               | 1              |
| 2               | 2              |
| 1               | 2              |
