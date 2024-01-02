---
layout: post
title: "How To: Delta Live Tables with Ask Databricks"
description: A Q&A on Delta Live Tables
image: 
  path: /assets/img/blog/spark.jpg
  srcset:
    1060w: /assets/img/blog/ask-databricks-1-1.png
    530w:  /assets/img/blog/ask-databricks-1-1@0,5x.png
    265w:  /assets/img/blog/ask-databricks-1-1@0,25x.png
sitemap: true
hide_last_modified: true
---

In a recent episode of [Ask Databricks](https://www.advancinganalytics.co.uk/askdbx){:target="_blank"} hosted by [Advancing Analytics](https://www.linkedin.com/company/advancing-analytics/){:target="_blank"}, special guest [Michael Armbrust](https://www.linkedin.com/in/michaelarmbrust/){:target="_blank"} joined for a Q&A on Delta Live Tables. Here are the key takeaways. Enjoy!


## 🚀 Can you use percentage run (%run) in a DLT pipeline? How do you extend your code base for DLT pipelines?
The magic command [percent run (%run)](https://docs.databricks.com/en/notebooks/notebook-workflows.html){:target="_blank"} isn't supported, but you can achieve similar functionality using pipelines – a collection of notebooks and files. For shared code, think standard Python packages or attaching Python wheels to your DLT pipeline. DLT gives you options!

## 🔧 Is Change Data Feed separate from CDC, or does it integrate into a CDC pipeline?
[CDC](https://www.databricks.com/blog/2021/06/09/how-to-simplify-cdc-with-delta-lakes-change-data-feed.html){:target="_blank"} captures changes between systems, and Delta tables have change feeds, streamlining this process. DLT simplifies schema evolution and ordering, a game-changer with APPLY CHANGES INTO, handling more than just SCD type 1.

## 🤔 How do you handle skeptical non-technical managers when convincing them of using DLT?
"DLT boosts productivity and slashes operational costs." Explaining how DLT streamlines pipeline management and enhances parallelism can ease concerns, delivering value from data faster.

## ⚙️ Is there an upper limit to the number of tables in a DLT? When do you start breaking things up into smaller pipelines?
Recommendation: 10s to 100s of tables per DLT pipeline - though this heavily depends on the tables. The Spark driver will be the first to cause problems. Fix by increasing the driver memory. Beyond that, consider partitioning into separate pipelines for efficiency and scalability.

## 🛠️ What are the best practices for Medallion Architecture and DLT?
Understanding the nuances of [streaming tables and materialized views](https://docs.databricks.com/en/delta-live-tables/index.html){:target="_blank"} is key. Streaming prioritizes performance, while materialized views ensure correctness for transformations. Choose the right tool for the job!

## 🛡️ Development best practices? How to test a DLT pipeline? Can you work locally?
Always use version control and break up logic into sources and transformations. Testing on Databricks itself is crucial since DLT doesn't run locally yet. Create a separate testing environment for thorough testing. Tip: use Databricks Bundle Assets (currently in Public Preview) to easily deploy to various environments. For more info, see this blog post on software dev and DevOps for DLT by Databricks.

## 📈 What’s the performance difference between SQL and Python in DLT?
Performance difference is negligible. SQL and Python result in the same performance due to Spark SQL's logical query planning. Python is great for metaprogramming (e.g., creating 10 tables in a loop), while SQL UDFs are efficient for certain operations (they're often combinations of already vectorized SQL functions).

## 💡Any plans for a GUI for developing? A point-and-click interface?
If you desire a GUI, let your Databricks Representative know! That being said, while GUIs are great for demos, they can be challenging for real-life collaboration and version control.

## 🔄 Is it possible to run a table with all its downstream and upstream dependencies?
Currently, the [Refresh Selected](https://docs.databricks.com/en/delta-live-tables/updates.html){:target="_blank"} feature allows selecting tables to refresh in a DLT pipeline. However, direct dependency selection isn't supported. [personal side note: dbt does offer this capability using the plus sign: dbt run --select +my_table+]

## 🛠️ When would you use dbt or DLT?
You can use both! Use [DLT](https://www.databricks.com/product/delta-live-tables){:target="_blank"} for streaming tables or materialized views and add [dbt](https://www.getdbt.com/){:target="_blank"} for SQL queries on top of those. In general, choose based on your specific use case and requirements.
