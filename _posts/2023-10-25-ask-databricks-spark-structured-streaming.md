---
layout: post
title: Structured Streaming With Apache Spark On Databricks
description: An Ask Databricks Q&A on getting started with Structured Streaming in Databricks
image: 
  path: /assets/img/blog/ask-databricks-1-4.webp
  srcset:
    1060w: /assets/img/blog/ask-databricks-1-4.webp
    530w:  /assets/img/blog/ask-databricks-1-4@0,5x.webp
    265w:  /assets/img/blog/ask-databricks-1-4@0,25x.webp
sitemap: true
hide_last_modified: true
---

Time for another video in the [Ask Databricks](https://www.advancinganalytics.co.uk/askdbx){:target="_blank"} series ([view on Youtube](https://www.youtube.com/watch?v=d905UJhIIHk){:target="_blank"})! This time, [Advancing Analytics](https://www.linkedin.com/company/advancing-analytics/){:target="_blank"} is joined by [Ray Zhu](https://www.linkedin.com/in/ray-zhu-67531245/?lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3BW7IeAndOSfarWAsBl61NzQ%3D%3D){:target="_blank"} to discuss [Structured Streaming](https://docs.databricks.com/en/structured-streaming/index.html){:target="_blank"}.

It's a lengthy video with an enormous amount of great insights, so let's 🐬 dive straight in!

## 🌊 What is structured streaming in Spark?

Structured Streaming is an **abstraction layer built on top of [Apache Spark](https://spark.apache.org/){:target="_blank"}**, designed to handle real-time data processing. It simplifies stream processing by **using the same familiar data frame API as batch processing**, blurring the lines between batch and streaming. This convergence in the industry responds to the growing demand for accessible and efficient stream processing, making it mainstream.

## 📦 Streaming versus micro-batch processing

Streaming in the context of Big Data can be understood in three main ways. Firstly, it involves near real-time processing, handling data within seconds or minutes. Secondly, it's about continuous processing as new data arrives, in contrast to batch processing. Thirdly, streaming is incremental and stateful, focusing on new data, not reprocessing the entire dataset. **The key distinction between streaming and batch is its statefulness and ability for incremental processing.** While some talk about "record by record" processing, the real improvement lies in the shift from sequential to asynchronous processing, enhancing efficiency in terms of latency and throughput. This improvement was missing in the early days of structured streaming but has since been implemented.

## 🔧 Spark Structured Streaming versus Delta Live Tables

In Databricks, Structured Streaming and [Delta Live Tables (DLT)](https://www.databricks.com/product/delta-live-tables){:target="_blank"} work together seamlessly. **DLT builds on top of Structured Streaming**, offering a declarative approach to stream processing. With DLT, developers can focus on data processing logic while the system handles infrastructure tasks, such as job scheduling and failure recovery. Databricks provides two runtime options: Delta Live Tables for fully managed ETL pipelines and [Databricks Jobs](https://docs.databricks.com/en/workflows/index.html#what-is-databricks-jobs){:target="_blank"} for structured streaming jobs, catering to different user preferences and workflows, with performance optimizations available.

## 📋 Checkpointing in Structured streaming and using Unity Catalog

In structured streaming using Apache Spark in Databricks, integration, especially [checkpointing](https://docs.databricks.com/en/structured-streaming/query-recovery.html){:target="_blank"}, is crucial for job runtime. The DLT Spark runtime layer is where the critical integration happens, ensuring better governance and reliability. The goal is to abstract away checkpointing complexities, so **users can focus on their streaming jobs without worrying about restarts or data corruptions**. State processing aims to restart without rebuilding from scratch, most likely using volume storage. This approach simplifies management in scenarios with numerous stream processing operations. It's essential to keep checkpointing separate from data flow to prevent accidental tampering and to provide access to specific checkpoint information for debugging and analysis without risking data corruption.

## 👐 Stream-to-stream joins

In Structured Streaming with Spark on Databricks, [stream-to-stream joins](https://www.databricks.com/blog/2018/03/13/introducing-stream-stream-joins-in-apache-spark-2-3.html){:target="_blank"}, particularly in scenarios with out-of-order data, rely on the concept of [watermarks](https://www.databricks.com/blog/feature-deep-dive-watermarking-apache-spark-structured-streaming){:target="_blank"} to synchronize and calculate results effectively. **Watermarks help manage the trade-off between latency and accuracy** by allowing you to delay the emission of results until a certain time period has passed. This balance between latency and accuracy is context-dependent, with **low latency being critical for applications like Netflix streaming and high accuracy for financial transactions**. However, you can leverage structured streaming to set up two different applications, one focusing on real-time low latency and the other on maintaining a complete copy of the data for accuracy, ensuring accurate results in analytical tasks while handling real-time workloads effectively.

## 🚫 Fault tolerance and rolling back in Spark structured streaming

In Structured Streaming with Spark on Databricks, **there are two key considerations for checkpoint management and data replay**. First, the platform aims to simplify checkpoint management to relieve users of this burden. For replay, it's important to understand the starting point from the data source, using offsets for systems like Kafka and state information for cloud storage. The more complex aspect is handling downstream data during replay, where Delta tables come into play. With Delta, you get idempotent characteristics and exactly-once semantics, eliminating the need to worry about data removal before replaying. It also ensures accurate results when using materialized views, simplifying the process and shifting the focus to downstream data management, addressing potential challenges effectively.

## 📂 File arrival and job triggering

In Structured Streaming with Spark on Databricks, you can **trigger processes through manual, scheduled, upstream event, or continuous methods**. While all these approaches aim to achieve the same goal, continuous processing is the ideal target, as it minimizes costs. The core capabilities being developed involve cluster selection, auto scaling, and serverless management, eliminating the need for users to worry about infrastructure details. **The long-term vision is to enable continuous processing**, so you only pay for compute when there's data to process, and abstract complexities for a seamless user experience. Databricks is already making strides in this direction with default machine selection, improved auto scaling, and forthcoming serverless capabilities. Simplifying the process for users is the ultimate goal.

## 💾 Reloading files after file changes

In Structured Streaming with Spark on Databricks, streaming sources like Kinesis, Kafka, and file-based sources primarily **follow an "append-only" approach**, treating changes as new writes for idempotency. For instance, even a small change in a file on Amazon S3 is seen as creating a new file from the streaming engine's perspective. **Delta simplifies this process by handling idempotency and supporting unique keys**, making it more efficient for handling updates without redundancy. When working with streaming data, keep in mind that modifications are essentially new writes, and deleting or modifying existing data is not allowed, sticking to the fundamental principle of appending new data in your data lake.

## 👷 Monitoring and debugging streaming applications

Databricks has made significant strides in enhancing observability for ETL workloads. **With the introduction of event logs, monitoring and debugging data is stored as a Delta table**, simplifying the debugging process. Users running Structured Streaming jobs can benefit from the Spark UI, which provides insights into running tasks, latency, and processing metrics. Additionally, the streaming query listener API offers the flexibility to capture custom information during job execution. **Databricks is also actively working on facilitating data integration with third-party monitoring tools.**

## 📥 For each batch processing

In Structured Streaming with Spark on Databricks, the "for each batch" API is **primarily intended for specific, exotic use cases**. It's commonly used by those writing data into unsupported syncs, merging data from change streams, or handling data fanouts. However, the platform is actively working to simplify and optimize most workflows, reducing the necessity for "for each batch" and ensuring smoother data processing.

## ⛔ When to not use streaming

In the realm of Structured Streaming with Spark in Databricks, the choice to use streaming **largely depends on your specific data objectives**. If you require real-time processing or are handling ingestion workflows into Delta Lake, streaming is the way to go for efficiency and state management. For transformation tasks, **if low latency is your priority, streaming is ideal**. However, **if accuracy takes precedence over speed, batch processing, which includes utilizing materialized views or custom Spark jobs, may be the better option**. Ultimately, the choice between streaming and batch processing depends on your specific workload and priorities.