---
layout: post
title: Evaluating The Medallion Architecture
description: The best alternative to the Medallion architecture
image: 
  path: /assets/img/blog/medallion-architecture.webp
  srcset:
    1060w: /assets/img/blog/medallion-architecture.webp
    530w:  /assets/img/blog/medallion-architecture@0,5x.webp
    265w:  /assets/img/blog/medallion-architecture@0,25x.webp
sitemap: true
hide_last_modified: true
---

I love best practices ❤️ However, they have the potential to be blinding when followed dogmatically. Databricks' [Medallion architecture](https://www.databricks.com/glossary/medallion-architecture){:target="_blank"} is one such example. [This video](https://www.youtube.com/watch?v=fz4tax6nKZM){:target="_blank"} by [Advancing Analytics](https://www.linkedin.com/company/advancing-analytics/){:target="_blank"} does a great job explaining why that is, and how to approach the Medallion architecture. Here's a quick summary and my own two cents.

## Introduction

In the dynamic landscape of Data Lakes, the Medallion architecture has garnered increased attention. While the **simplicity of the Medallion architecture is beneficial for conveying its structure**, it's crucial to acknowledge that this model might **not be a one-size-fits-all solution**. The classification of (just three!) layers as "bronze," "silver," and "gold" oversimplifies the complexity, prompting debates on appropriate actions at each level.

## 🔍 What is the Medallion architecture?

In the traditional Medallion architecture, data is sourced from diverse channels and curated in a [Data Lake](https://www.databricks.com/discover/data-lakes){:target="_blank"} environment. **This process moves data through three layers of increased quality: bronze, silver, and gold.** The bronze layer contains raw, uncleaned data, while the silver layer involves validation and cleansing. Finally, the gold layer represents aggregated business-ready data, usually for analytics. Let's go over each layer in a little more depth.

## 🥉 Bronze

The initial layer, termed "Bronze," **handles raw data by storing it as-is**. For example, you may store your data in its original format, like Parquet or JSON, maintaining its original structure while being ready for Spark processing. **This layer serves as a checkpoint**, detached from the source system, allowing for subsequent validation against expected schema(s).

## 🥈 Silver

The Silver layer involves **data cleansing and validation**. Here we address issues like the creation or manipulation of columns, or primary key application. It's crucial for conforming and consolidating cleaned data from various sources.

## 🥇 Gold

The Gold layer encompasses **data modeling** and **aggregated, business-ready data**, focusing on creating fact and dimension tables (in case you're using a [STAR schema](https://www.databricks.com/blog/2022/05/20/five-simple-steps-for-implementing-a-star-schema-in-databricks-with-delta-lake.html){:target="_blank"}). Analytical models include layered aggregations, and tools like Power BI introduce a reporting layer.

## 🚫 Don’t dogmatically stick to the Medallion architecture

The separation into, and, more importantly, the use of the terms bronze / silver / gold **layers can enhance clarity and facilitate conversations** between users with varying backgrounds. After all, these terms make it easy to think about data quality and data purpose. **However**, it's important to note that adhering strictly to a three-tiered structure **might not suit every company's unique characteristics**. The Medallion architecture is designed to be flexible, recognizing that **not every aspect of operations needs to fit neatly into a single layer**. For businesses without standardized layers due to diverse source systems, conforming data across multiple sources may not be necessary, and that's perfectly acceptable.

## 💵 My two cents

So where does this leave us? **Ditch the bronze, silver, and gold all together?!** Hm... tempting, but no.

The Medallion architecture serves as a **valuable starting point for structuring Data Lakes** and organizing data processing workflows. Its strengths lie in providing a shared framework for teams to discuss and implement data curation practices. However, **it's important to recognize its limitations** and not view it as a one-size-fits-all solution.

**In practical terms**, organizations should approach the Medallion architecture with **their specific business needs in mind**. What is the nature of your data, what are the intricacies of you data processing pipelines? Embrace flexibility and adaptability, allowing for customization and refinement of the architecture to better align with your organization's unique context.

While the Medallion architecture may serve as a valuable guide, it's advisable to **supplement it with additional considerations**, such as industry-specific requirements, regulatory compliance, and the evolving landscape of data technologies. **The key is to strike a balance** between adopting a standardized approach for communication and remaining agile enough to accommodate the diverse and dynamic nature of modern data management.