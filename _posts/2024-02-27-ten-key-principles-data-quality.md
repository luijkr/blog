---
layout: post
title: Ten (minus one) Key Principles For Data Quality
description: Why data quality is more than quality data
image: 
  path: /assets/img/blog/data-quality.webp
  srcset:
    1060w: /assets/img/blog/data-quality.webp
    530w:  /assets/img/blog/data-quality@0,5x.webp
    265w:  /assets/img/blog/data-quality@0,25x.webp
hide_last_modified: true
---

I was once asked a simple question during a job interview: **"what constitutes data quality?"** Surely that must have been an easy question to answer. After all, **we all have a gut feeling** of what quality data is. Or at least most of us will have a sense of what bad data looks like. And yet it stumped me. Why was I unable to just give a **comprehensive and cohesive answer?**

Turns out I never questioned what exactly defines data quality. **Its definition seemed obvious,** and could ultimately be expressed in terms of metrics and numbers indicating the amount of `NULL` values in a column. You know, things you can display in a dashboard that no one ever looks at. 😉

**I was wrong.** Data quality is much more than a few superficial metrics indicating what quality data is. For example, getting data ready on time, and making it is useful to the business also play a huge rol in data quality. Put differently: **data quality does not simply equal quality data.**

## (Some Of) The Pillars of Data Quality

Upon pondering the deceivingly simple question after the interview, I came up with a few principles that can I divided up  according to three questions:

- Do the data an accurately represent the reality it intends to portray? (I promise this won't get too philosophical 😉)
- How useful is the data to its users?
- How timely is the data?

The principles I'll lay out below don't necessarily provide a definitive definition of data quality. It's also not an exhaustive list, but at least it's a start.

Each principle is illustrated using the same **example: a hypothetical online retailer.** Any one will do. Got one in mind? Good, let's go.

### 1. Does the data accurately represent the reality it intends to portray?

These principles pertain to the values themselves. A classic example would be `NULL` values, or missing values.

#### Accuracy

Do the data values accurately **represent the real-world entities** they are meant to reflect?

The online retailer maintains a database of product prices. An inaccuracy occurs when the **listed price of a product does not match the actual price at checkout.** Any customer would be at least surprised by this, and probably dissatisfied.
{:.note}

#### Precision

Precision in data refers to its **level of detail.** High precision ensures that the data values are specific and not overly generalized.

Customer preferences are recorded for personalized recommendations in the online store. However, **if the data only captures broad product categories** without considering specific attributes, such as color or brand, the resulting **recommendations may lack precision.** Consequently, these less accurate recommendations may not be as relevant to customers.
{:.note}

#### Validity

**Valid data adheres to pre-set rules and constraints.** Checks for data validation aid in ensuring that data follows expected formats, ranges, and conditions.

During the checkout process, customers are required to enter their shipping addresses. Implementing **address validation checks ensures the validity of shipping information,** reducing delivery issues and avoiding customer frustration.
{:.note}

#### Completeness

Complete data contains all **the information needed for a specific use case or analysis.** Missing data can lead to biases, thus impairing the efficiency of decision-making processes.

Customers have the option to review their purchases. However, if a **substantial number of product reviews are missing or incomplete,** it may be difficult for decision-makers to accurately gauge customer satisfaction.
{:.note}

### 2. How useful is the data?

While it's great that all data is stored in your favorite database and modeled using the latest techniques, it's essential to consider whether this data is truly helpful to its consumers.

#### Usability

Usable data is displayed in **a format that is comprehensible and easy to work with.** This involves well-structured datasets, clear documentation, and user-friendly interfaces for accessing and modifying the data. The definition of 'user-friendly' varies depending on the end user. For instance, the data needs of developers differ from those of the sales department.

The BI engineer delivers complex sales reports to the marketing team. Without **clear labels** or **structure**, it becomes hard to extract meaningful information, possibly abandoning the dashboard.
{:.note}

#### Relevance

**Relevant data aligns with the organization's goals** and objectives or those of a specific project. Irrelevant data can create noise and detract from key insights.

Our online retailer tracks browsing behavior, but for a marketing campaign focused on demographics, **data like device type may be irrelevant.** By focusing on demographics, the dataset aligns more with the project's goals.
{:.note}

#### Integrity

Data integrity ensures that **relationships between different data elements are maintained.** For example, if data in one part of the dataset references data in another part, the integrity of these relationships must be preserved.

Online retailers store product and order data. **Maintaining data integrity is key to associating each order with the correct product,** as discrepancies could result in shipping incorrect items to customers.
{:.note}

### 3. When is the data updated?

Infrequent one-time data dumps are seldom sufficient. The **timely updating of data with the latest information** is essential for numerous business processes. When is this update typically performed?

#### Timeliness

Timely data is up-to-date and **reflects the current state of affairs.** Outdated information may lead to obsolete analyses and decisions based on inaccurate or irrelevant data.

Any online retailer relies on inventory data to manage stock levels efficiently. **If the inventory data is not updated** in real-time or near real-time, there's a **risk of overselling products** that are no longer in stock. This is especially crucial during peak shopping periods.
{:.note}

#### Consistency

Consistent data means that similar data elements are uniform and follow **the same format and conventions throughout the dataset.** Inconsistencies can lead to confusion and errors during analysis.

Oftentimes, online retailers use a combination of internal and external data sources to track customer demographics. **Inconsistencies in how age or income data is formatted** (e.g., different date formats, varying units of currency) can hinder the integration and analysis of this information.
{:.note}

## Data Quality Is Not Simply Quality Data

There you have it.

Quality data, when defined simply in terms of missing values (or lack thereof) or having as much data as possible stored somewhere, often is not enough. Various other factors also play a huge role in data quality.

The above principles are by no means a guarantee for perfect data. Rather, they aim to provide some **guidance to achieve data that is correct, timely, and useful** for the business.

Just because you have quality data sitting somewhere, doesn't mean data quality in the broad sense has been achieved. There's more to it.
