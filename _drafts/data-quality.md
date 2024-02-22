---
layout: post
title: Why Data Quality Is More Than Quality Data
description: Ten (minus one) key principles for high quality data
image: 
  path: /assets/img/blog/data-quality.jpg
  # srcset:
  #   1060w: /assets/img/blog/data-quality.webp
  #   530w:  /assets/img/blog/data-quality@0,5x.webp
  #   265w:  /assets/img/blog/data-quality@0,25x.webp
hide_last_modified: true
---

In a recent job interview, I was asked a simple question: _"what constitutes data quality?"_. Surely that must have been an easy question to answer. After all, we all have a gut feeling of what quality data is. Or at least most of us will have a sense of what _bad data_ looks like. And yet it stumped me. Why was I unable to just give a comprehensive and cohesive answer?

Turns out I never questioned my own notion of data quality. The definition of data quality seemed obvious, and could ultimately be defined in terms of metrics and numbers. You know, things you can show in a dashboard that no one ever looks at. 😉

I was wrong. Data quality is much more than the metrics indicating what quality data is.

## The Pillars of Data Quality

Upon pondering the deceivingly simple question after the interview, I came up with a few principles that can be divided up according to three questions:
- Do the data measure what they are supposed to measure?
- How useful is the data?
- When is the data updated?

These principles don't necessarily provide a definitive definition of data quality. This is also not an exhaustive list, but at least it's a start.



### Do the data measure what they should measure?

These principles pertain to the values themselves. A classic example would be `NULL` values, or missing values. As another example, consider academics, where measurement error is a big deal.

#### Accuracy

Are the data values correct and do they reflect the real-world entities they represent?

The online retailer maintains a database of product prices. An inaccuracy occurs when the listed price of a product does not match the actual price at checkout. This can lead to customer dissatisfaction and potential revenue loss. Ensuring accurate pricing information is crucial for building trust with customers.
{:.note title="accuracy example"}

#### Precision

Precision refers to the level of detail in the data. High precision ensures that data values are specific and not overly generalized.

The online retailer tracks customer preferences for personalized recommendations. If the data captures only broad categories of products without considering specific attributes like color, size, or brand that customers care about, the recommendations may lack precision. Enhancing precision in customer preference data allows the retailer to offer more tailored and relevant product suggestions.
{:.note title="precision example"}

#### Validity

Valid data conforms to predefined rules and constraints. Data validation checks help ensure that the data adheres to the expected formats, ranges, and conditions.

During the checkout process, customers are required to enter their shipping addresses. If the system does not validate these addresses against a standard format or fails to check for common errors, such as typos or missing postal codes, it may result in undeliverable packages. Implementing address validation checks ensures the validity of shipping information, reducing delivery issues and customer frustration.
{:.note title="validity example"}

#### Completeness

Complete data includes all the necessary information required for a particular use case or analysis. Missing data can introduce biases and limit the effectiveness of decision-making processes.

The online retailer collects data on customer feedback for products, including ratings and reviews. If a significant portion of product reviews is missing or incomplete, decision-makers may not have a comprehensive understanding of customer satisfaction. Ensuring completeness in customer feedback allows the retailer to make informed decisions, identify areas for improvement, and provide a more holistic view of product performance.
{:.note title="completeness example"}


### How useful is the data?

It's great that all the data is stored in your favorite database. It's also modeled according to the latest modeling techniques. But is it actually useful?

#### Usability

Usable data is presented in a format that is easy to understand and work with. This includes well-organized datasets, clear documentation, and user-friendly interfaces for accessing and manipulating the data.

The online retailer provides sales reports to its marketing team for strategic planning. If these reports are presented in a convoluted format, without clear labels or intuitive organization, it becomes challenging for the marketing team to extract meaningful insights. Improving the usability of data involves creating well-designed dashboards and reports that facilitate easy interpretation and analysis, ultimately supporting more effective decision-making.
{:.note title="Usability example"}

#### Relevance

Relevant data is aligned with the goals and objectives of the organization or a specific project. Irrelevant or extraneous data can introduce noise and distract from the key insights.

The online retailer collects data on website visitors' browsing history, including pages visited and time spent on each page. However, for a specific marketing campaign focused on customer demographics, irrelevant data such as the device type used by visitors may introduce noise. Filtering out irrelevant data and focusing on customer demographics aligns the dataset with the project's goals, ensuring that the analysis is more targeted and meaningful.
{:.note title="relevance example"}

#### Integrity

Data integrity ensures that relationships between different data elements are maintained. For example, if data in one part of the dataset references data in another part, the integrity of these relationships must be preserved.

The online retailer stores data on product inventory and customer orders. Maintaining data integrity is crucial to ensure that each order is associated with the correct product information. If there is a discrepancy between the product details in the inventory and the corresponding order records, it can lead to shipping the wrong products to customers. Implementing data integrity checks and validation mechanisms helps uphold the consistency and accuracy of relationships between different data elements.
{:.note title="integrity example"}



### When is the data updated?

Rarely will a one-off data dump be enough. Updating data with the newest data is crucial for many business processes. When is that done?

#### Timeliness

Timely data is up-to-date and reflects the current state of affairs. Outdated information may lead to obsolete analyses and decisions based on inaccurate or irrelevant data.

The online retailer relies on inventory data to manage stock levels efficiently. If the inventory data is not updated in real-time or near real-time, there's a risk of overselling products that are no longer in stock. Timely updates to the inventory system help ensure that the retailer is aware of current stock levels, preventing issues such as backorders or delayed shipments. This is especially crucial during peak shopping periods.
{:.note title="timeliness example"}

#### Consistency

Consistent data means that similar data elements are uniform and follow the same format and conventions throughout the dataset. Inconsistencies can lead to confusion and errors during analysis.

The online retailer uses a combination of internal and external data sources to track customer demographics. Inconsistencies in how age or income data is formatted (e.g., different date formats, varying units of currency) can hinder the integration and analysis of this information. Enforcing consistent formatting and conventions for data elements across the dataset ensures that analysts can seamlessly combine and compare data, reducing the risk of errors and promoting a unified understanding of customer demographics.
{:.note title="consistency example"}

## Data Quality Culture: Why No One Looks At Your Dashboard

### Leadership and Accountability

Stress the importance of leadership in fostering a culture of data quality.
Highlight the role of individuals in various roles in maintaining data accountability.

### Training and Education

Advocate for ongoing training programs to keep teams informed about best practices.
Discuss the value of educating employees on the impact of data quality on their work.

## Section 4: Technical Solutions for Data Quality

### Data Quality Tools

Introduce popular tools that aid in maintaining data quality.
Highlight features and benefits without getting too technical.

### Data Governance

Explain the concept of data governance and how it contributes to data quality.
Discuss the role of policies, standards, and procedures.

### Conclusion

Summarize the key points made throughout the blog post.
Reinforce the idea that investing in data quality is an investment in the success of data-driven initiatives.

## Further resources

Encourage readers to share their thoughts on data quality and their experiences.
Prompt them to explore further resources on data quality or share the blog with their network.
Remember to use a conversational tone and incorporate visuals such as charts or infographics to make the content more engaging. This approach should resonate well with a LinkedIn audience that includes both technical and non-technical professionals.