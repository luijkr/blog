---
layout: post
title: Batch Jobs Are Dead, Long Live Batch!
description: Rethinking batch jobs in the post-"Batch is Dead" era
image: 
  path: /assets/img/blog/twilight.webp
  srcset:
    1060w: /assets/img/blog/twilight.webp
    530w:  /assets/img/blog/twilight@0,5x.webp
    265w:  /assets/img/blog/twilight@0,25x.webp
hide_last_modified: true
---

Nietzsche once famously proclaimed that *["Gott ist tot (God is dead)"](https://en.wikipedia.org/wiki/God_is_dead)*. In the present day, traditional batch processing - while once reigned supreme, now faces a similar fate - it’s dying.

At least that’s what people have been saying for years: *["batch jobs are dying"](https://particular.net/blog/death-to-the-batch-job)*, *["why are you still doing ETL"](https://medium.com/@BillScottCoder/why-are-you-still-doing-batch-processing-etl-is-dead-3dac2392a772)*. And with the meteoric [rise of streaming](https://www.datanami.com/2023/07/12/yes-real-time-streaming-data-is-still-growing/), how could you possibly think otherwise?

**Confession:** I *do* there’s a place for batch processing - though not in the way that it has traditionally existed.

Batch processing involves the processing of data in predefined intervals or batches, where data is collected, processed, and analyzed as a group at scheduled intervals. Streaming processing, on the other hand, involves the continuous and real-time processing of data as it is generated, enabling immediate analysis and response to incoming data streams.
{:.note title="Batch processing vs. streaming"}

## The rise of real-time processing

Technology has advanced quite a bit. Systems are now able to **continuously *generate* data.** At the same time - partly due to customer demand, it has also become possible to ***process* this data in real time.** 

For example, consider **sensors monitoring critical machinery** in a factory in order to detect or prevent mechanical failures in these machines. Or look at how **social media routinely collect data on user behavior** (clicks, views, etc.) used for better recommendations, ideally both in (near) real time.

It’s easy to see how batch processing in the above two examples would not suffice. Let’s go over some of the disadvantages of batch processing that streaming focused data processing addresses.

## The problem with batch processing

**Latency.** The most important downside to batch processing is *latency*. Batch processing typically operates on fixed intervals, meaning there is an **inherent latency between data generation and analysis.** Coming back to online recommendation engines: if we can immediately process the last watched video by a user, then we can update any recommendations made to this user in (near) real time. TikTok does this extremely well, which has contributed to its popularity.

**Data freshness.** Related to latency is data freshness. Stale data is inherent to batch processing, leading to **insights based on data collected in the past.** Decision-making in dynamic environments where up-to-date information is crucial needs access to timely data.

**Scalability.** While batch processing is meant to deal with large chunks of data, **increasing data volumes could still lead to scalability issues.** This is particularly true if a batch job was created some time ago without the original job being designed to handle a steady increase of data over time. Processing increasingly larger datasets within constrained time windows can lead to longer processing times and limited resources for other jobs.

**Complexity.** Designing, managing, and troubleshooting **batch processing pipelines can be complex** and time-consuming. Handling their dependencies, managing job scheduling, and ensuring fault tolerance in batch workflows is difficult. Doing this well requires careful planning, and changing requirements to these jobs require maintenance.

## Rethinking batch processing in the post "batch is dead" era

Okay, so batch *isn’t* dead, but its supreme reign *does* seem to have ended - or at least something has changed. So **what kind of twilight zone is batch processing in?** To answer that question, let’s first go back to what made batch so attractive in the first place.

### Why batch processing was/is used

**Historical analysis.** Batch processing has been a go-to choice for **looking at past data.** Retrospective analysis is often used to find trends, patterns, and useful insights. A lot of companies still depend on this method to make big decisions and predict future trends.

**Data warehousing and ETL.** ETL in data warehousing environments often still requires batch processing. These tasks often involve **processing massive datasets** in a cost-effective and efficient manner.

**Resource optimization.** In scenarios where data arrival is not time-sensitive or where real-time processing is not necessary, **batch processing can be more resource efficient.** By aggregating and processing data in batches, resources can be optimized, thus reducing costs.

**Regulatory compliance.** In regulated industries such as finance, healthcare, and government, batch processing may be preferred for compliance reasons. Batch jobs allow for easily **maintaining audit trails**, ensure data integrity, and **meet regulatory requirements** for data retention and processing.

**Complex analytics.** Certain types of complex analytics, such as deep learning model training on large datasets, can be more efficiently performed using batch processing. **Batch jobs provide stability and repeatability,** making them a good option for tasks that require extensive computational resources and long processing times.

**Large Language Models.** Though related to the previous point, LLMs certainly added to the demand for batch processing. Training such models costs a significant amount of resources, and is just not suitable for stream processing.

### Long live batch!

Batch processing has been popular for a good reason - multiple reasons actually, just look at the list above. However, as a data processing paradigm **it is feeling the pressure from changing demands and streaming technologies.** To meet these demands, batch processing has evolved in several ways.

#### Micro-batch processing

One of the ways in which batch processing has evolved is by introducing *micro-batches*. Micro-batch processing is still similar to regular batch processing - they both process groups of records at a time. The key difference being that **micro-batch processing handles smaller batches - but much more frequently.** This significantly decreases the latency - from hours to minutes.

It should be noted that anything approaching a latency of minutes might be quite expensive. After all, you’re almost continuously running queries in your data warehouse. This probably isn’t as efficient - and compute power definitely is not cheap.
{:.note title="Cost of micro-batch processing"}

Ironically, this shift to micro-batches has **blurred the lines between batch processing and streaming.** Indeed, several popular frameworks are able to handle both. [Apache Spark Streaming](https://spark.apache.org/docs/latest/streaming-programming-guide.html) - and more recently [Databricks Delta Live Tables](https://www.databricks.com/product/delta-live-tables) - is a prime example of being able to handle frequent micro-batches - and continuous streaming processing obviously.

#### Additional improvements

- **Enhanced fault tolerance.** Fault tolerance is a big deal. Automatic retries, checkpointing, and recovery mechanisms prevent failures and disruptions of the data flow. Batch processing systems are becoming more resilient to failures and disruptions by incorporating advanced fault tolerance mechanisms. Techniques such as **checkpointing, job [retries](https://learn.microsoft.com/en-us/azure/databricks/workflows/jobs/settings#--configure-a-retry-policy-for-a-task), and automatic recovery mechanisms** help ensure data integrity and job completion even in the presence of failures.
- **Improved frameworks for creating batch jobs.** Low(er) code solutions such as [Azure Data Factory](https://learn.microsoft.com/en-us/azure/data-factory/introduction) provide an easy way to create pipelines. Data ingestion, transformation, and storage can be achieved using a graphical interface.
- **Integration with streaming technologies.** Batch processing frameworks are increasingly integrating features that allow for **hybrid batch-stream processing.** Again, Databricks comes to mind. This enables the transition of workloads between batch and streaming modes, providing flexibility in data processing.
- **Improved scalability.** The improved scalability capabilities of batch processing frameworks allow handling ever-growing datasets. This includes enhancements in **distributed computing** and **parallel processing** (*e.g.,* [Apache Spark](https://spark.apache.org/)), the **serverless model** (*e.g.,* [AWS Fargate](https://aws.amazon.com/fargate/), [Databricks Serverless Compute](https://docs.databricks.com/en/serverless-compute/index.html)), and resource management to efficiently process large volumes of data within a shorter time frame.

## Final thoughts

Streaming obviously has taken a significant portion of the spotlight. However, the use case is just not always there, especially when your data has already reached a data warehouse. As such, I think batch jobs will persist, albeit in a continuous state of evolution, poised to coexist alongside streaming in the data engineering space.
