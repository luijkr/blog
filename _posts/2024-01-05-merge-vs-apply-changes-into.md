---
layout: post
title: Merge vs. Apply Changes in Databricks
description: How to effectively use Apply Changes for Change Data Capture
image: 
  path: /assets/img/blog/apply-changes.jpg
  srcset:
    1060w: /assets/img/blog/apply-changes.jpg
    530w:  /assets/img/blog/apply-changes@0,5x.jpg
    265w:  /assets/img/blog/apply-changes@0,25x.jpg
hide_last_modified: true
---

In SQL, the `MERGE` statement is a familiar tool in the toolkit of any data specialist, frequently employed for managing [Change Data Capture (CDC)](https://learn.microsoft.com/en-us/azure/databricks/delta/delta-change-data-feed){:target="_blank"}. Unsurprisingly, the power of `MERGE INTO` extends into the [Databricks environment](https://docs.databricks.com/en/sql/language-manual/delta-merge-into.html){:target="_blank"}. However, the use of `MERGE` for CDC data presents its own set of challenges.

Imagine this scenario: since our last check of the CDC feed in the original database, **a single record may have undergone multiple changes**. Managing these changes in the correct order becomes a crucial consideration. Furthermore, crafting the logic to handle distinct operation types, such as `INSERT`, `UPDATE`, or `DELETE`, falls squarely on our shoulders.

This is where `APPLY CHANGES` steps in to simplify the process!

# `MERGE` redefined: `APPLY CHANGES`

Luckily, within the context of Delta Live Tables (DLT) **there's a much simpler way of doing what's essentially a complicated `MERGE`**. The folks at Databricks gave it a different name, `APPLY CHANGES`, to distinguish it from a regular `MERGE`.

In a nutshell, `APPLY CHANGES` is a **declarative way in Databricks Delta Live Tables that simplifies handling CDC** by applying changes from a source table to a target table. It's worth noting, however, that there are subtle differentiators setting `APPLY CHANGES` apart from the conventional `MERGE` statement.

## Comparing `MERGE` with `APPLY CHANGES`

While `MERGE` serves as a versatile tool for merging or updating data across tables, `APPLY CHANGES` is specifically tailored for use within Delta Live Table (DLT) pipelines. It's important to note that the source table can be a regular Delta table, but **the target table must be a Delta Live table**.

What sets `APPLY CHANGES` apart is its specialized capability to handle CDC data seamlessly. This means not only accommodating updates but also gracefully **managing multiple updates to the same row**, even when they occur out of order—a truly noteworthy feat. We'll delve deeper into this impressive functionality shortly.

# `APPLY CHANGES` syntax

Upon browsing through the [documentation](https://learn.microsoft.com/en-us/azure/databricks/delta-live-tables/cdc){:target="_blank"} of `APPLY CHANGES`, we notice the syntax is somewhat familiar to `MERGE`, yet still different enough to warrent further exploration. In the above docs, the following example command is given. Let's go over each line to get a better understanding of what's happening.

```sql
APPLY CHANGES INTO
  live.target
FROM
  stream(cdc_data.users)
KEYS
  (userId)
APPLY AS DELETE WHEN
  operation = "DELETE"
APPLY AS TRUNCATE WHEN
  operation = "TRUNCATE"
SEQUENCE BY
  sequenceNum
COLUMNS * EXCEPT
  (operation, sequenceNum)
STORED AS
  SCD TYPE 2
```

## Naming

Pretty obvious, but the naming is different. The folks at Databricks deliberately named it different to distinguish between a regular `MERGE` and `APPLY CHANGES`.

## Matching using `KEYS`

The `KEYS` keyword is used to define the columns for matching. The expectation is a list of at least one column that **must exist in both the source and target tables.** By comparison, in a `MERGE` command, a straightforward `JOIN`-like condition can be stated, where the key(s) to join on are specified.

Interestingly, `APPLY CHANGES` introduces a separation of the keys and an optional filter by having a distinct `WHERE` clause, separate from the `KEYS`. This extra `WHERE` caues the update only to be applied when the specified condition is satisfied.

## Deleting records using `APPLY AS DELETE`

When working with CDC data, it's common to encounter a column in the incoming data that signifies the type of operation performed in the source database — commonly `INSERT`, `UPDATE`, or `DELETE`. Here we specify the conditions under which we want to apply a `DELETE`.

Note that in the `APPLY CHANGES` statement, **the default behavior is an `UPSERT`**. This eliminates the need for explicit specification of `INSERT` or `UPDATE` statements, improving readability.

## Ordering mutations using `SEQUENCE BY`

The `SEQUENCE BY` keyword is a powerful tool in `APPLY CHANGES` that handles scenarios where multiple edits, such as updates or deletes, are associated with the same primary key or a combination of specified columns in the target table. `SEQUENCE BY` only expects a column that determines the order in which to handle multiple updates (usually a timestamp of the mutation). `APPLY CHANGES` then handles the rest under the hood.

## Selecting which `COLUMNS` to `INSERT` or `UPDATE`

Rather than explicitly listing all columns in separate `UPDATE` or `INSERT` statements, users can efficiently specify the target columns with the `COLUMNS` keyword. Moreover, this approach allows for a reverse scenario where users articulate the columns they prefer not to update using `COLUMNS * EXCEPT`.

## Creating a target table

A pivotal step involves the creation of a target table. This is accomplished through the straightforward command `CREATE STREAMING TABLE <table-name>`. This command operates without the need for a predefined schema. While its precise functionality may not be explicitly outlined in the documentation, it's reasonable to assume that it verifies the existence of a Delta Live table first, before creating one. Note that failing to include this command in your workflow results in a pipeline failure.
