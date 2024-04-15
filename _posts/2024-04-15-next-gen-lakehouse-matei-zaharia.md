---
layout: post
title: How Generative AI Within Databricks Improves Our Engineering Lives
description: Databricks CTO Matei Zahari discusses generative AI
image: 
  path: /assets/img/blog/nextgenlakehouse.webp
  srcset:
    1060w: /assets/img/blog/nextgenlakehouse.webp
    530w:  /assets/img/blog/nextgenlakehouse@0,5x.webp
    265w:  /assets/img/blog/nextgenlakehouse@0,25x.webp
hide_last_modified: true
---

NextGenLakehouse have a great [newsletter on Substack](https://nextgenlakehouse.substack.com/){:target="_blank"} and their own [YouTube channel](https://www.youtube.com/@nextgenlakehouse){:target="_blank"}. They recently had Databricks CTO [Matei Zaharia](https://www.linkedin.com/in/mateizaharia/){:target="_blank"} on to discuss the Databricks platform and how Generative AI will make all of our lives that much easier 🙂

This post covers the main points of the interview. If you want to check out the full video, you can find it [here](https://www.youtube.com/watch?v=OeIc1nCBcAg){:target="_blank"}.

## 🎯 Current focus: Databricks platform and generative AI development.

In the past, Matei Zahari has worked on [Apache Mesos](https://mesos.apache.org/){:target="_blank"}, [Apache Spark](https://spark.apache.org/){:target="_blank"}, and [MLFlow](https://mlflow.org/){:target="_blank"}. Currently, he is focused on two key areas: **enhancing [Unity Catalog](https://www.databricks.com/product/unity-catalog){:target="_blank"} and governance** for improved data sharing - crucial for customer satisfaction. In addition, he spends his time on **Generative AI research** to develop models with enhanced capabilities, specifically for large enterprises.

## 🧬 Databricks' evolution: Spark ➡️ ML ➡️ Lakehouse ➡️ Modern data governance platform.

The **initial focus of Databricks was to address specific data challenges,** particularly in areas where existing tools fell short. This led to a strong emphasis on large-scale ETL and data transformation - laying the groundwork for building a comprehensive data platform. As cloud computing and the demand for machine learning and data science took off, Databricks **expanded its scope to include features like [Lakehouse](https://www.databricks.com/product/data-lakehouse){:target="_blank"} storage and governance** functionalities to meet these needs.

Furthermore, as data governance requirements grew more complex **with the emergence of new regulations and AI use cases,** Databricks recognized the necessity for a more sophisticated solution. The **development of Unity Catalog (UC)** reflects this evolution. UC provides support for intricate policies, ensuring compliance with ever-evolving data privacy regulations and best practices.

![Databricks logo history](/assets/img/blog/databricks-logo-history.webp){: width="75%" style="display: block; margin: 0 auto" }
Databricks' logo history.
{:.figure}

## 🏠 Defining data governance in 2024

There are two critical aspects for managing data effectively: *cataloging* and *flexible policies*. **Cataloging involves understanding what data is available,** what its source is, and making sure the data complies with rules regarding its usage and storage. Flexible policies are essential for adapting to changing requirements. Additionally, **fine-grained policies at the row and column level** enable more precise governance beyond file-level policies in a traditional data lake.

In addition, **understanding the origin of data** within the Databricks platform is key. There is a need to know where data originates, and what its associated constraints and intended purposes are. This includes considerations such as geographic limitations and specific use cases, with access permissions tailored accordingly. This is part of a shift towards a more nuanced approach. This approach to **data access is not solely based on user privileges but rather on the intended purpose,** ensuring data is used appropriately for its intended tasks - *e.g.,* fraud detection.

## 😦 Customers top concerns at the enterprise level

The biggest challenge many organizations face is **effectively managing and leveraging their data**. This is often hindered due to complexities in data governance, access control, and quality assurance. Despite having rich datasets, the intricacies of handling policies often restrict access and hinder using the data across the company.

**Potential solutions** include implementing features like **automatic [tagging](https://docs.databricks.com/en/data-governance/unity-catalog/tags.html){:target="_blank"}, [lineage tracking,](https://docs.databricks.com/en/data-governance/unity-catalog/data-lineage.html){:target="_blank"} and request for access workflows.** These tools should make data classification easier, enhance visibility into sensitive information (*e.g.,* PII). A difficult task, as facilitating *controlled* access to ensure data remains secure while also enabling broader utilization within the organization seems like an impossible balancing act.

## 🆘 Challenges around integrating Generative AI

A key challenge around Generative AI is **ensuring data privacy and security,** particularly as models may inadvertently **memorize sensitive information during training.** To address this, there is a growing interest in techniques like masking (*e.g.,* of PII) before training any models. Additionally, there's a need for **AI-driven analysis to identify** and filter out **spam or sensitive content** within large text datasets.

Databricks addresses these challenges with **AI functions in SQL, enabling efficient batch processing for tasks like record filtering.** Databricks is also developing a suite of standard functions for tasks such as entity extraction and sentiment analysis. This should help users cleaning their data before it's fed into generative applications or model training.

## 📖 How MosaicML fits into data governance and Unity Catalog

Databricks is advancing its platform with features like **automatic data tagging**, allowing users to efficiently tag and set policies on incoming data through AI analysis. This capability is expected to **evolve into a suite of [built-in AI functions](https://docs.databricks.com/en/large-language-models/ai-functions.html){:target="_blank"}**, continuously improving over time. Additionally, the platform offers **UI assistance**, not only for coding tasks but also for **understanding and debugging governance policies**. Imagine having a conversational model that can provide insights and recommendations on governance issues, helping users navigate their inherent complexities.

![MosaicML](/assets/img/blog/mosaicml.webp){: width="75%" style="display: block; margin: 0 auto" }
Databricks aquired MosaicML in 2023.
{:.figure}

## 🧙‍♂️ How Generative AI and data governance help Databricks overcome challenges

**Databricks has long believed in the convergence of data and AI tasks**, offering a unified engine, data store (*i.e.,* [Delta Lake](https://docs.databricks.com/en/delta/index.html){:target="_blank"}), and governance model. This approach simplifies the management of data sources and helps in policy-setting and downstream impact analysis across various AI applications. Moreover, the integration of generative AI within this unified platform creates a **better understanding of data usage for diverse applications**, fostering continuous improvement and better outcomes.

In essence, Databricks' approach emphasizes the **strong relationship between AI and data within the unified platform**. Databricks extends its capabilities to external data stores through features like [query federation,](https://docs.databricks.com/en/query-federation/index.html){:target="_blank"} providing users with a single point of access.

## 🧐 Defining the Data Intelligence Platform

The concept of a data platform is evolving towards a broader framework termed the *"[data intelligence platform](https://www.databricks.com/product/data-intelligence-platform){:target="_blank"}"*. This **includes technologies like the Lakehouse and various AI tools**. Data intelligence involves the platform understanding the semantics of data, helping users in navigating and querying this data more effectively. Generative AI plays a role in this by not only assisting in error debugging, but also by **analyzing data usage patterns**. It’s not just data platform users that are helped by Generative AI, applications built on top of the platform also benefit from understanding data semantics. **This integration of AI and data is essential** given the complexity of modern data platforms and the growing need for efficient use of data across organizations.

## 🪄 Generative AI simplifies coding and enhances governance

The Databricks platform is improving its [AI assistant](https://www.databricks.com/product/databricks-assistant){:target="_blank"}, particularly regarding error diagnosis. With AI features enabled, users are given hints and pointers, and even automated fixes when encountering errors. Whether during interactive use within the SQL editor or a notebook, or when addressing production job failures in real-time, this functionality **promises efficiency gains and potentially alleviates the burden of manual intervention**.

Moreover, Databricks is **advancing towards more intuitive search and discovery capabilities**, alongside the evolution of low-code interfaces. As an example, consider the ability to construct dashboards simply by inputting commands, as demonstrated in LakeView dashboards. This approach not only facilitates rapid dashboard creation but also promotes sharing of these dashboards and even natural language querying.

## 🤖 AI will take our jobs!

Despite advancements in code generation and data intelligence, the role of data engineers and scientists will persist. However, their **focus will shift from lower-level coding tasks towards more complex conceptual and business problems**. Certain questions related to data analysis require more context that cannot be given by AI. For example, insights from various stakeholders within the organization are needed - such as the CFO or the legal department, in order to effectively address business problems. So **no need to worry, AI won’t take your jobs**. Data professionals will continue to play an important role in providing the business with meaningful analyses, albeit with less emphasis on coding tasks and more on providing insightful answers to pressing business questions.
