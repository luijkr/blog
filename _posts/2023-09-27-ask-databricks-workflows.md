---
layout: post
title: "Go With The Flow! How To: Delta Live Tables with Ask Databricks"
description: A Q&A on Databricks Delta Live Tables
image: 
  path: /assets/img/blog/ask-databricks-1-2.jpg
  srcset:
    1060w: /assets/img/blog/ask-databricks-1-2.jpg
    530w:  /assets/img/blog/ask-databricks-1-2@0,5x.jpg
    265w:  /assets/img/blog/ask-databricks-1-2@0,25x.jpg
sitemap: true
hide_last_modified: true
---

Another [Ask Databricks](https://www.advancinganalytics.co.uk/askdbx){:target="_blank"} episode hosted by [Advancing Analytics](https://www.linkedin.com/company/advancing-analytics/){:target="_blank"} launched! 🚀 This time, [Roland Fäustlin](https://www.linkedin.com/in/roland-f%C3%A4ustlin-1544465b/){:target="_blank"} joined to discuss Orchestration using [Workflows](https://docs.databricks.com/en/workflows/index.html){:target="_blank"}. Let's dive in! 🐬

## 💡 What is Databricks Workflows? How does it differ from a Job?

Workflows is the pipeline orchestrator that schedules and runs different Jobs, which in turn are collections of tasks. Workflows orchestrates various jobs, managing any interdependencies that may exist.

## 💼 How does Workflows compare to Airflow, another popular orchestrator?

Workflows is a tool designed to integrate seamlessly with Databricks and facilitate job execution. Compared to [Apache Airflow](https://airflow.apache.org/){:taret="_blank"}, Workflows offers advantages such as easy integration with Databricks, being a fully managed service, and providing CI/CD support through [Databricks Asset Bundles](https://docs.databricks.com/en/dev-tools/bundles/index.html){:target="_blank"}, making it a comprehensive solution within the Databricks ecosystem.

## 🛠️ User segmentation

Jobs are often segmented based on user type, with analysts leaning towards SQL and embracing Workflows. The tool is evolving to cater to data engineers, making it more versatile and appealing across all user segments.

## 🔄 Migrating Workflows between environments, CI/CD, and testing

[Databricks Asset Bundles](https://docs.databricks.com/en/dev-tools/bundles/index.html){:target="_blank"} streamline workflow migration and deployment, allowing easy source control integration, simplifying CI/CD and testing processes.

## 🔧 External Triggers and Integration

You can already trigger workflows externally from various orchestrators like [Apache Airflow](https://airflow.apache.org/){:taret="_blank"}. Just use the [Jobs API](https://docs.databricks.com/api/workspace/jobs){:target="_blank"}.

## 🌟 Best Practices when using an external orchestrator

For efficient operations, creating a workflow within Databricks is recommended, leveraging benefits like cluster reuse between tasks, easy debugging, and seamless code editing. Triggering this Workflow should be easy from any external orchestrator.

## ⚙️ Workflows and Delta Live Tables

Workflows and [Delta Live Tables](https://www.databricks.com/product/delta-live-tables){:target="_blank"} complement each other. Workflows is great for orchestrating control flows (task 1 first, then the second, etc.). Delta Live Tables optimizes this control flow for you with the end goal in mind. In short, Workflows focuses on control flow, whereas DLT focuses on data flow.

## 📊 Monitoring and Management

Efficiently manage workflows by analyzing metrics, detecting patterns at Workflow, Job, and Task levels. Additional features like Tags provide insights into costs per workflow group, aiding in effective monitoring and control.

## 🔄 Making Workflows Dynamic

Jobs already are highly parameterizable, allowing dynamic parameters at the Job level and at the Task level (so-called task values, similar to Apache Airflow's [XComs](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/xcoms.html){:target="_blank"}). This enables conditional branching and creating meta-jobs, making workflows more dynamic and adaptable.

## 🛡️ Integration with Unity Catalog

Workflows seamlessly integrate with [Unity Catalog](https://docs.databricks.com/en/data-governance/unity-catalog/index.html){:target="_blank"}, allowing lineage tracking and triggering based on data changes in Delta tables and triggering based on file arrival, optimizing processes and reducing costs.

## 🌊 Streaming Jobs with Workflows

For streaming jobs, DLT offers flexible options for batch or continues [streaming processing](https://docs.databricks.com/en/structured-streaming/index.html){:target="_blank"}. In the case of continuous streaming jobs, Workflows provides automated restarts, ensuring no loss of data.

## 🌐 Orchestrating External Tasks

Though orchestrating external taks is already possible today, Databricks aims to make make it even better. Expanding this feature, Databricks will integrate more partners for smoother processes, such as sending emails or triggering jobs in external orchestration tools.

## 🚀 Future Focus - Serverless

Anticipating the future, the team is most excited about serverless capabilities, envisioning a future where manual cluster sizing becomes a thing of the past, saving time and costs.
