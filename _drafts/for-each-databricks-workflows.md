---
layout: post
title: For Each In Databricks Workflows
description: One For Each, Each For All!
image: 
  path: /assets/img/blog/for-each-workflows.webp
  srcset:
    1060w: /assets/img/blog/for-each-workflows.webp
    530w:  /assets/img/blog/for-each-workflows@0,5x.webp
    265w:  /assets/img/blog/for-each-workflows@0,25x.webp
hide_last_modified: true
---

It’s finally here! The long-awaited feature of *for loops* is [available in Databricks Workflows](https://www.databricks.com/blog/streamlining-repetitive-tasks-databricks-workflows){:target="_blank"}. This allows you to **neatly create multiple tasks based on a list of input values**. I finally had time to check it out and have a go at it myself, so let’s see it in action!

## Running A Parameterized Notebook

What are we trying to achieve exactly? As an example, we want to run a parameterized notebook in Databricks. This notebook **takes a single parameter `country`** and prints it:

```python
country = dbutils.widgets.get("country")
print(country)
```

Simple stuff. How can we use Workflows to call the above code for multiple countries?

### 💾 Level 0: Back In the Olden Days

Previously, we had to **manually create separate tasks** for these. Assuming we have **three different countries** we want to run this for, **the job would have three tasks**.

![Level 0 Job](/assets/img/blog/for-each-level-0.png){: width="75%" style="display: block; margin: 0 auto" }
Databricks Job with three manually created tasks, each using a different value for the same `country` parameter
{:.figure}

This works just fine. Going into the result of the first task, we see **it successfully printed the input `country` parameter**.

![Level 0 Task Output](/assets/img/blog/param-task-run-0.png){: width="75%" style="display: block; margin: 0 auto" }
Output of a task running a parameterized notebook
{:.figure}

Manually creating three instances of the same task is a **bad practice**, and cumbersome at best. Altering anything about this task would require us to *change all three tasks manually*. In addition, **managing dependencies between tasks becomes more difficult**.

*How can we improve this?*

### ⌨️ Level 1: For Each, But With Hardcoded Task Values

Instead of manually creating these tasks as in *Level 0*, we want to use the newly introduced *For Each* task type. This can be achieved using a **two-step approach**, where we **create a parent task** and a **child task** to execute multiple times.

**First, create a task of the type *For each***. Note how for the *Inputs* field, I manually specify a JSON like object to loop over. This will make sure our notebook is run three times, as I’ve listed three input values here.

![Level 1 Job](/assets/img/blog/for-each-level-1.png){: width="75%" style="display: block; margin: 0 auto" }
Defining a *For Each* task using hardcoded input values
{:.figure}

Next, within this parent task, **define another child task to execute**. Note how in the UI the inner (child) task is now selected.

This **child task will be executed once for each element** in the *Inputs* field. Which parameterized notebook to use is specified in the child task. More importantly, we also **specify the parameter to pass to the notebook**. Here we use the **`{% raw %}{{ input }}{% endraw %}` notation to indicate the current element of our input array** - taken from the *Inputs* option listed in the parent task.

![Level 1 Job Child Task](/assets/img/blog/for-each-level-1-child-task.png){: width="75%" style="display: block; margin: 0 auto" }
Child task of a *For Each* parent. The same `country` parameter is used
{:.figure}

This creates a job with three input parameters that we can run. Running it indeed shows three tasks - as expected.

![Task runs for child tasks](/assets/img/blog/for-each-level-1-tasks-run.png){: width="75%" style="display: block; margin: 0 auto" }
Three child tasks run as part of a *For Each* parent task
{:.figure}

Just as with any other type of task, it's possible to **go into the output of each task individually** to see the expected `print` statements being executed.

## 🪄 Level 2: Generate Task Values Programatically

In the above example, **we hardcoded the values for the *Inputs* field** using three country names. While this works, it is **only a small improvement over manually creating three tasks** - everything’s still hardcoded.

Instead, we should define the parameters elsewhere, making the job more flexible. To achieve this, **create another notebook setting so-called [task values](https://docs.databricks.com/en/jobs/share-task-context.html){:target="_blank"}**, which can then be utilized by the *For Each* task.

```python
values = ["The Netherlands", "United States", "Australia"]

dbutils.jobs.taskValues.set(key="countries", value=values)
```

The job below now looks almost identical to the one created for Level 1, except that we have added an extra step at the beginning. This extra step sets the task values. In addition, the value for the *Inputs* option is also slightly different. We now **use the `countries` task values set in the `Set_Parameters` task**. Referencing each element in the inner child task remains the same - *i.e.,*, {% raw %}`{{ input }}`{% endraw %}.

![Level 2 Job](/assets/img/blog/for-each-level-2.png){: width="75%" style="display: block; margin: 0 auto" }
Task values set in the *Set_Parameters* task are accessed in the *Input* field
{:.figure}

### 🧙‍♂️ Level 3: Nested For Each Loops

A logical next step would be to use nested for loops. For example, within each country we also want to loop over some of its cities. This is **not natively supported in Workflows**. However, as a workaround, we could **use *For Each* to call another job**. Given the input below, we would create a second job - also containing a *For Each* task - looping over the provided cities.

```python
values = [
  {
    "country": "The Netherlands",
    "cities": ["Amsterdam", "Rotterdam"]
  },
  {
    "country": "United States",
    "cities": ["New York", "Los Vegas"]
  },
  {
    "country": "Australia",
    "cities": ["Canberra", "Sydney"]
  }
]

dbutils.jobs.taskValues.set(key="countries", value=values)
```

When you’ve gotten this far, *you now truly are a wizard, Harry!* 😉

## Limitations And Considerations

There are several limitations and things to consider when using the *For Each* task type.

### Single Task

*For Each* **only allows a single task to be looped over**. An orchestrator like Azure Data Factory (ADF) *does* allow [looping over multiple tasks](https://learn.microsoft.com/en-us/azure/data-factory/control-flow-for-each-activity){:target="_blank"}, which are then run in sequence. Airflow is even more flexible, and allows all kinds of customer structures - *e.g.*, using [branching](https://www.astronomer.io/docs/learn/airflow-branch-operator){:target="_blank"}.

Of course, a notebook could execute many steps, but it would have been nice to separate different steps in separate tasks.

### Nested Loops

Nested loops are **not supported** by Workflows - nor is it by ADF. As mentioned in Level 3, a workaround is to **use an outer *For Each* loop to call another job**.

### Concurrency

While not mentioned in this blog post, a *concurrency* parameter can be set for a *For Each* task - defaulting to 1. **The maximum concurrency is 100**, which should be plenty for most use cases. Do be mindful of how many tasks you want to run in parallel.

### Running Tasks Sequentially

When the concurrency parameter is set to anything greater than the default of 1, it will run as many tasks as possible in parallel. This implies that **we can also run things sequentially** - just set the concurrency parameter to 1. However, in that case the **order in which your tasks are executed depends on how you define the task values**. Pay attention to how you define your parameters and you're good to go.
