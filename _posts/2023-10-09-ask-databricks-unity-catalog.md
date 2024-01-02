---
layout: post
title: One Ring To Rule Them All! Databricks Unity Catalog
description: 
image: 
  path: /assets/img/blog/ask-databricks-1-3.jpg
  srcset:
    1060w: /assets/img/blog/ask-databricks-1-3.jpg
    530w:  /assets/img/blog/ask-databricks-1-3@0,5x.jpg
    265w:  /assets/img/blog/ask-databricks-1-3@0,25x.jpg
sitemap: true
hide_last_modified: true
---

Continuing their [Ask Databricks](https://www.advancinganalytics.co.uk/askdbx){:target="_blank"} series, [Advancing Analytics](https://www.linkedin.com/company/advancing-analytics/){:target="_blank"} released yet another video ([view on Youtube](https://www.youtube.com/watch?v=qW83cFSS5dA){:target="_blank"}) full of top-notch insights! 🥇 This time, [Paul Roome](https://www.linkedin.com/in/paulroome/?lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3By8d%2FCop8TlKisdHEA85lkw%3D%3D){:target="_blank"} joined to discuss [Unity Catalog](https://www.databricks.com/product/unity-catalog){:target="_blank"}, a one-stop governance shop for all your data and AI objects.

Enough talking, let's dive in! 🐬

## 💍 One ring to rule them all!

[Unity Catalog](https://www.databricks.com/product/unity-catalog){:target="_blank"} is a metadata management and governance tool designed to help organize, discover, and govern your data and analytics assets within the Databricks environment. It provides a centralized repository to manage metadata and facilitate collaboration and data lineage tracking, including your ML models. Think of it as your go-to solution to tailor who gets access to what within your organization. Different strokes for different folks!

## 🔄 Sharing data between metastores and regions

Data can be shared between metastores, but not between regions. The reason for not allowing access between regions is that customers often are very intentional about this. It is still possible to share data across regions through Delta sharing, which makes this type of sharing very intentional.

## 🛣️ End-to-end data lineage with Unity Catalog

Data lineage is a neat feature for data governance, and Unity Catalog has got it covered. Simply write your code, and Unity Catalog automatically creates a clear visual graph showcasing the lineage. It's not just about data tables; it tracks ML models too. That way you can truly see the (entire) picture!

## 🔍 Automatically identifying Personally Identifiable Information (PII)

[Lakehouse Monitoring](https://docs.databricks.com/en/lakehouse-monitoring/index.html){:target="_blank"} within Unity Catalog is leveling up. It's not just about monitoring models anymore; the team is diving into data quality, including automatically detecting PII. Smart, efficient data management is on the horizon!

## 🏗️ Best practices for managing objects using Unity Catalog

Use a structured approach by aligning the Catalog to specific data domains or data types. Think of it as a way to organize your digital world. For example, store all your sensor data in one Catalog. Add a [Software Development Life Cycle (SDLC)](https://www.databricks.com/blog/applying-software-development-devops-best-practices-delta-live-table-pipelines){:target="_blank"} environment to your Catalog name to make it more specific (e.g., `sensor_dev` or `sensor_prod`). Lastly, choose the right owner to further structure and maintain your data home! 

## ❓Managed tables versus external tables

[Which kind of table should you use?](https://docs.databricks.com/en/data-governance/unity-catalog/create-tables.html){:target="_blank"} As is often the case, it depends on your game plan! Managed tables are like the "easy mode" button, while external tables offer customization for defined data. But guess what? The perks of managed tables are slowly making their way to external tables. More flexibility, more options!

## 🏢 Setting up Unity Catalog in an enterprise environment

Try not to do everything at once, it's a phased approach! Think identity models, table setups, and a gradual migration of data consumers. Slow and steady wins the Unity Catalog race, ensuring a smooth transition!

## 🏎️ Unity Catalog by default

In large organizations, finding the right admin for Unity Catalog can be a challenge. How can we overcome this hurdle? Luckily, Databricks is simplifying the process! In the near future, Unity Catalog will be seamlessly integrated into Workspace creation, making it the default setup. Smooth sailing ahead! ⛵

## 🚦 Attribute-based access control (ABAC)

ABAC is on the radar! Combining row and column level access controls and tags in Unity Catalog is the first step. Every company is unique, and ABAC offers a versatile way to achieve data governance that fits like a glove!

## 🌟 Unity Catalog and Microsoft Fabric

Exciting times ahead! Databricks is collaborating closely with Microsoft to seamlessly integrate Unity Catalog with Azure Fabric. Centralized data management and discovery in one hub - the future looks promising!

## 🏠 Governance with Generative AI Models

Tracking ML models using Unity Catalog is already possible. Data lineage concerns are even more importent with Large Language Models and generative AI. Unity Catalog creates insight into the entire data lineage for these models, ensuring compliance with evolving regulations.

## 📈 Delta Live Tables Integration

[Delta Live Tables](https://www.databricks.com/product/delta-live-tables){:target="_blank"} and Unity Catalog synergize by allowing users to define and manage Data Lake Table (DLT) pipelines effortlessly, all DLTs being governed by Unity Catalog. While users define lineage within a DLT pipeline, Unity Catalog extends this lineage to its broader usage, providing comprehensive visibility of the pipeline and its tables within your broader data architecture.

## 💾 Best Practices for Backup and Recovery

Unity Catalog offers an open metadata structure, enabling users to tailor backup and disaster recovery strategies to their specific needs. Existing methods like metadata dumps and restoration into Workspaces can be automated through APIs, and future updates aim to simplify these processes even further.

## 🌊 MLFlow Integration

Unity Catalog seamlessly integrates with [MLFlow](https://www.databricks.com/product/managed-mlflow){:target="_blank"}, allowing users to store and manage models as assets within the catalog. This integration resolves a significant challenge previously faced with MLFlow by enhancing the model registry's functionality and integrating it comprehensively within the end-to-end data lineage.

## 💽 Understanding Volumes

[Volumes](https://docs.databricks.com/en/sql/language-manual/sql-ref-volumes.html){:target="_blank"} in Unity Catalog serve as a vital mechanism for managing access to unstructured data stored in external locations, such as paths in cloud storage like S3. These high-level entities can be further organized into tables and volumes, offering controlled access to specific data subsets, improving data management granularity.

## 🔮 Exciting Upcoming Features

In the short term, Unity Catalog is introducing read-only catalog bindings, allowing seamless access to production catalogs from development environments. Looking ahead, exciting prospects include cross-region, cross-cloud, and cross-system governance, aiming for an expansive, cohesive data governance framework. This vision is underpinned by access control based on Attribute-Based Access Control (ABAC) rules, robust governance reporting, and a marketplace for streamlined data discovery.
