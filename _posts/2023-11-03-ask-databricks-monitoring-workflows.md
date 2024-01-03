---
layout: post
title: "Keeping An Eye Out: Monitoring Databricks Workflows"
description: An Ask Databricks Q&A on monitoring Databricks Workflows
image: 
  path: /assets/img/blog/ask-databricks-1-5.jpg
  srcset:
    1060w: /assets/img/blog/ask-databricks-1-5.jpg
    530w:  /assets/img/blog/ask-databricks-1-5@0,5x.jpg
    265w:  /assets/img/blog/ask-databricks-1-5@0,25x.jpg
sitemap: true
hide_last_modified: true
---

Another day, another [video](https://www.youtube.com/watch?v=PSCxaQKj-6M){:target="_blank"} in the [Ask Databricks](https://www.advancinganalytics.co.uk/askdbx){:target="_blank"} series! Workflows were already the topic of a previous video in this series (for my TLDR, see [this post](https://www.linkedin.com/pulse/go-workflow-ask-databricks-round-two-ren%25C3%25A9-luijk/)). This time, however, [Advancing Analytics](https://www.linkedin.com/company/advancing-analytics/){:target="_blank"} is specifically exploring **_monitoring_** your Workflows.

As usual, let's dive straight in! 🐬

## 🔍 Main features of monitoring Workflows

When dealing with large-scale workflows in Databricks, it can become challenging to keep track of hundreds or even thousands of jobs from various sources. To effectively monitor and identify what to focus on, Databricks provides features like the **[Jobs Runs](https://docs.databricks.com/en/workflows/jobs/monitor-job-runs.html){:target="_blank"} page**. This page offers a **comprehensive list of all job runs**, with a graph showing recent changes in pass/fail rates, new jobs, and quick access to error reports. **Filtering options**, such as "Active Runs", allow you to pinpoint ongoing tasks and assess their progress. By drilling into specific job runs, you can **quickly identify failed tasks**, their execution times, and any associated error messages. This proactive approach helps administrators, even those without complete control, spot potentially problematic jobs, making workflow management more efficient.

## ⛔ Troubleshooting job failures

To efficiently monitor workflows in Databricks, **start by filtering for failed runs within the last 48 hours**, which is a useful default time frame for many users. By clicking on the "start time" on the left, quickly access the details of the failed run, including any error messages. In the case of multi-task runs, pinpoint the specific task that failed and view the associated errors at the top. To gain context and locate the error within your notebook, **click on "highlight error"** to scroll directly to the relevant cell. This allows you to understand the error within the context of your notebook, similar to when you ran it interactively.

## 🏗️ Managing workflows across multiple workspaces

Monitoring workflows in Databricks can be challenging, as there isn't built-in cross-workspace monitoring. Instead, it's recommended to **leverage the [system tables](https://docs.databricks.com/en/administration-guide/system-tables/index.html){:target="_blank"} product**, particularly the audit logs, billing logs, and soon-to-be-released job logs and job run logs. These logs provide a comprehensive overview of activity across workspaces, enabling the creation of personalized Databricks SQL dashboards and the setup of alerts for suspicious events. System tables offer a foundation to build your monitoring infrastructure, helping you identify issues at a high-level and then delve into specific workspaces for detailed job monitoring.

## ⚠️ Integrate Databricks SQL alerts with external systems

Databricks SQL alerts **offer versatile destinations**, such as email with dashboard snapshots and links for notifications. Workflow alerts cover failures, successes, and starts, with the recommendation to configure at least a failure notification via email, Slack, or Teams. These apps can be ideal for critical jobs to ensure swift visibility and prevent costly, lingering issues.

## 🔍 Organize Databricks jobs with tags for efficient management

It's highly advisable to **leverage job tags** when monitoring workflows in Databricks. These tags can be applied as key-value pairs or simple labels, providing a **flexible way to organize and filter your job list**. By using tags effectively, you can easily label and filter data by teams or other categories, making it a valuable tool for workflow management. Databricks is continuously enhancing tag-based filtering, so expect more improvements in the near future.

## 🏁 Resuming a failed job from the point of failure

One of the standout features in Workflows is the **"repair and rerun" functionality**. When dealing with failed jobs, it allows you to easily navigate to the error, offering a repair button at the top of the screen. This feature is highly efficient as it **enables you to resume from the point of failure without re-running successful tasks**. This is particularly useful for fixing notebooks or addressing transient issues, and manual initiation of repairs has proven to be successful most of the time, making it a widely used and effective solution for handling data-related problems.

## ➡️ Triggering a job from another job

Databricks recently introduced the **Run Job Task**. It enables a push-based approach to start subsequent jobs, promoting code modularization and decoupling, especially in collaborative environments. While it's not the sole method for breaking down jobs, it's highly valuable. Keep an eye out for more trigger types in the future!

## 🪲 Apache Airflow job monitoring and debugging within Databricks workflows

When it comes to monitoring jobs in Workflows, Apache Airflow jobs operate differently from classic Databricks jobs. You won't see them in the jobs or workflows lists, but you can find them in the runs list. **Airflow jobs are essentially one-time runs**, so if you're using Airflow regularly, you'll find them in the failed runs section. While you won't get the full historical view or Matrix view for these jobs, you can **access details about each individual run**. This approach makes job runs more visible for users coming from different orchestration systems, aiming to provide a seamless experience, regardless of the orchestrator being used.

## ➰ Loops within Databricks Workflows

The Databricks team is actively working on loops within Jobs, so **expect it to be available for early previews beginning of next year**. It will offer valuable features such as parallelization controls, dynamic list handling, cluster reuse, and more.

## 💻 Serverless and Workflows

**Serverless workflows in Databricks are in the early stages**, with a limited customer base during the early preview. The team is actively expanding access, continuously refining the product to ensure it's user-friendly and effective. Serverless is a top priority, with ongoing efforts to enhance and scale the offering, but there's no specific release date available yet.

## 🤷 Comparing Workflows monitoring with competitors' features

**Databricks Workflows are designed to be user-friendly, offering a low-code approach for both technical and non-technical users**. They can be created entirely through the UI. I’m addition, Workflows offers flexibility with JSON, YAML. A Python SDK for those who prefer a Python-based approach will be available soon, similar to Airflow. This approach aims to cater to the diverse preferences of different users within a data team, ensuring everyone can work comfortably within their chosen interface.

## 📈 Effectively analyzing and monitoring Databricks Workflow performance

**For historical analysis and monitoring workflows in Databricks, system tables are an excellent option.** While external integrations with tools like DataDog and Splunk are possible, they can be more challenging to set up due to data transfer issues, cost, and networking complexities. Databricks focuses on native ease of use and efficient data transfer to cater to specific use cases and streamline the monitoring process.

## 🖥️ Monitoring data quality

Databricks is excited about the [Lakehouse Monitoring](https://docs.databricks.com/en/lakehouse-monitoring/index.html){:target="_blank"} project, which allows you to **register specific tables for monitoring**. It processes statistics, **including profile and drift metrics**, and stores the results in Unity Catalog. Pre-generated SQL-based dashboards are provided for common analysis. In the near future, expect enhanced data classification, LLM monitoring, and unify expectation frameworks in collaboration with ML teams at Databricks.

## 👨💼 Managing environmental variables for consistent job deployment across environments

**Databricks Asset Bundles offer a powerful way to manage and segregate deployments** to development, QA, and production environments. You can easily set overrides, like using a dedicated cluster for faster Dev runs while using specific job clusters in production or QA. Plus, it ensures that when you push to the Dev workspace, your workflows remain paused to prevent unintentional scheduling of production workloads. **This feature provides robust control over environment variables** and is continually improving with enhanced integration with source control systems like GitHubs.

## 🔮 (Upcoming) features to look out for

In Databricks, there are three key features to enhance your workflow monitoring:

1. **Task-Level Notifications:** You can now configure task-level notifications with various integrations like Slack, PagerDuty, Microsoft Teams, and generic webhooks. It's recommended to set up these notifications, especially for failure cases, to proactively stay informed about your tasks.

2. **Duration Thresholds:** Databricks has introduced duration thresholds, allowing you to **set warnings for tasks that may take longer than expected**. This helps you receive notifications when something seems suspicious, without necessarily canceling the task. You can tie these warnings to various messaging platforms for effective monitoring.

3. **Continuous Streaming Workloads:** Databricks now offers a continuous trigger type for streaming workloads, ensuring uninterrupted operation. It's particularly useful for long-running streaming jobs, preventing email storms in case of issues and providing exponential back-off for retries.

Additionally, Databricks is working on table triggers to further enhance workflow management, promoting decoupled workflows and efficient data processing. These improvements aim to simplify and streamline notifications for smoother data operations.

## 🔑 Key advice for effectively monitoring Workflows in Databricks

The most crucial step in monitoring Databricks workflows is to **set up at least failure alerts for your jobs**. You can easily achieve this by creating a bash script using the CLI to add notifications to each job and task. **This will help you quickly identify non-functioning jobs** and proactively address any issues. It's essential to ensure that job creators are notified of failures, as many users may not have this feature enabled by default.