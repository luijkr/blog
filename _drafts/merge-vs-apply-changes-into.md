---
layout: post
title: Merge vs. Apply Changes in Databricks
description: How to effectively use Apply Changes in your Delta Live Table pipeline
hide_last_modified: true
---

In SQL, `merge` is a fairly common command that's in any data specialist's arsenal. Therefore, it shouldn't come as a surprise that `merge into` is also available in [Databricks](https://docs.databricks.com/en/sql/language-manual/delta-merge-into.html){:target="_blank"}. However, within the context of Delta Live Tables (DLT), there's another way of doing what's essentially a `merge`. The folks at Databricks gave it a different name though, `apply changes`, to distinguish it from a regular `merge`. There are a few additional differences though! Most importantly, `apply changes` is meant to handle Slowly Changing Dimensions (SCD) data. We'll dive deeper into the subtleties of `apply changes` and how it can simplify handling especially CDC data in your DLT pipelines.

# What is a `merge` statement in SQL?

At its core, a `merge` statement is a SQL command that combines the functionality of multiple operations: `insert`, `update`, `delete`. The resulting `merge` statement is a single, atomic statement. This unique capability allows users to synchronize data across tables quite efficiently. Rather than crafting separate queries for each operation, a single `merge` statement is written that does all of the above by reading the data just once, enhancing both readability and performance of your queries.

## Handling Slowly Changing Dimensions with `merge`

A common use case of `merge` statements is implementing Slowly Changing Dimensions (SCD). SCD is a way of tracking historical changes to dimension data. For an in-depth explanation of the different types of SCD, see this [excellent overview](https://playbook.microsoft.com/code-with-dataops/capabilities/analytical-systems/data-distribution/data-modeling/slowly-changing-dimension/){:target="_blank"}. The `merge` statement facilitates the management of versioning and historical data, enabling a smooth transition between different states of a record in your table.

Let's assume we have a `source` table and `target` table with SCD Type 2 data, where each row is identified by a unique `id`. The way we would incorporate the new data in our `source` table would be to use a `merge` statement, making sure to update any `valid_from` and `valid_to` as well to indicate a row's validity.

```sql
merge into target as t
using source as s
    on t.id = s.id
when matched and s.some_value != t.some_value then
    update set t.valid_to = getdate()
when not matched then
    insert(id, some_value, valid_from, valid_to)
    values(s.id, s.some_value, getdate(), NULL)
```

# `merge` redefined

## Handling CDC data


Upon browsing through the [documentation](https://learn.microsoft.com/en-us/azure/databricks/delta-live-tables/cdc){:target="_blank"} of `apply changes`, we notice the syntax is familiar, yet different. Let's rewrite our `merge` statement as `apply changes`, and then go over each line to get a better understanding of what's happening.

```sql
create or refresh streaming table target;

apply changes into live.employee
from stream live.new_data
keys (EmployeeID)
apply as delete when operation = "delete"
apply as truncate when operation = "truncate"
sequence by sequenceNum
columns * except (operation, sequenceNum)
stored as scd type 2;
```

## Technical differences

### `merge` to `apply changes`

As mentioned earlier, the folks at Databricks decided to give a different name to the standard `merge` statement, and rename it `apply changes`. The main point of distinction between a SQL `merge` statement and an `apply changes` statement lies not only in the naming convention but also in the abstraction. While the SQL `merge` statement closely adheres to the ANSI standard, the `apply changes` statement serves the same purpose of upserting data but is named differently to avoid confusion. The `apply changes` statement is essentially an abstraction that writes a merge statement for you, making it more intuitive and consistent within the Databricks environment.

# merge vs apply changes into

We're in DLT and we want to do an upsert
randomly. We want to do a
merge, it's not called a merge statement anymore. And there's a real
decision about that right, because they
didn't want it to be confusing when
you're writing a Spark SQL merge
statement that's deliberately built to
be very very similar to ANSI standard merge statement.
It looks and feels like any other SQL merge
statement and has the same syntax and
same operators.
Because this is an abstraction on top of
that that's actually writing a merge
statement for you they didn't want you
to write merge and then have to remember
that you're doing the DLT version of
merge. So they called it
something completely different.
So you
apply changes from a source into the target table by joining on a specific
key and with specific conditions. Then you specifcy what
to do when it matches and when it doesn't match. This is all the
same familiar stuff that you see inside a regular merge statement.

# table types of target and source

so i want to apply changes into
my target table
from my source table again both delta
live tables
one of them cannot be normal timing
we can kind of
mix and match i think in terms of the
source that can be coming from a normal
table uh but we're assuming we're going
into a dlt table.

# arguments

## keys

and then keys how should it work out
well if the record already exists or not
which is the key to joining essentially
it's our merge constraint.
and they've separated out two things so
you've got the where condition,
to say so this is the key to join and
see if it exists
but only when it satisfies this
condition should you actually apply the
update,
whereas previously i mean in a normal
merge statement you can jam that into
one big essentially join condition.
so there's no a separate thing saying this
is the name of the column that has to
appear on both sides so if we say this
is my primary key then my source
incoming data has to have a column
called primary key my target table has
to have a column called primary key and
it's going to automatically just write a
join assuming both sides have that same
column.
so keys has been simplified to make it easy
but also put some conditions on you and
that both sides have to have the same
column.

## IGNORE NULL UPDATES

ignore the updates don't bother updating
if nothing's changed


## APPLY AS DELETE WHEN condition

we've got sequence by
now sequence by is really interesting and
there's two two different things in
there.
so firstly it is the
it allows you to rerun the merge
um which is a massive thing.
so if you got three changes at once and
the same record the same primary key the
same record id three times in the set.
normally if you try and merge that into
emergency it goes no
it's not gonna work. in this case it's
actually sort of handling that by taking
that some kind of ordering, some kind of
modified date, update date, system time
dates, and allowing you to actually sort
of pile them up and access or work out
which is the most recent record,
therefore which should get applied.
so it has that in there. it also allows
you to um
take a look at should we bother updating
this is it going to have changed well
what's the sequence?
no that date's the same we'll treat this
record as not having changed
so this is interesting bits and pieces
by the nature of how they've written
this, as to what it means if you give it
a different record but has the same idea
in the same sequence number not going to
update it.
so a couple of catches to get used to
but actually some really useful
functionality in there.

## COLUMNS [columnList]

and then we can say
here's a list of columns that should be
updated so you don't have to update
every single column in your table.. you
can say bring these changes in apply all
the actual data column changes but don't
change my audit data of when i
originally loaded this thing i want that
to stay in there so i've got a record.
you can do things like that allows for
slowly changing patterns if you want to
lock down certain keys.
and you've also got on the other side
the except update everything except that
column because i want to keep that
column that's mine.


# apply changes into in python

okay then on the python side again
following that same thing it's not a
merge so we're no longer doing the go get a
delta table and do a 
deltatable.merge is what we'd
normally do for writing a normal delta
merge. and now we're doing apply changes,
we're just running an apply change
function. and then that has a certain
things it's asking for the target, makes
sense, the source,
the keys it should join on, the sequence
by all the same stuff we saw in sql just
in python mode.

## create target table

now there's one little gotcha that
normally uh gets people when they're
writing merge statements is if you're
trying to write something really super
generic and you can onboard a new table
and throw it through that same script
and it'll get some typo merge it in and
it's all good
unless the table doesn't exist.
um in which case it's you have to end up
having little if statements going in
just check if see if it exists if it
doesn't exist create a blank empty delta
table that i can then merge into
um and it's something we've built a
hundred times right
uh
and you have to kind of do a similar
thing here.
but the syntax is just a little bit
confusing when you first get to it. so
the python sample that they've got
so saying import dlt import some sql
functions that's fine.
uh grab
an existing delta live tabale
delta li table view by streaming over
this existing table fine happy
then we've got this dlt.create_target_table function
now i can dig around and i can't
actually find a definition for that
anywhere.
so just taking it on faith that that
makes sense and does a thing but we can
go and have a look at what that actually
does under the hood.
um so yeah it's essentially we're saying
this table the target the table named
target is defined by "create it if it
doesn't exist" eventually and then we're
doing a merge dlt apply changes merge my
data go into that target table which
again creative doesn't exist take my
source table which again is this we
defined it as slc in this view up there
assume that both sides have this user id
sequence by my sequence number
do this if it says it's delete then you
delete it
don't update my operation by secret
number so it's got essentially similar
commands