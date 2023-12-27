---
layout: post
title: Unit Testing PySpark Pipelines Using pytest
description: Yet another guide testing PySpark
hide_last_modified: true
---

PySpark, an open-source Python library by Apache, has gained immense popularity in data engineering and data analysis. Leveraging Apache Spark, it efficiently processes large datasets in distributed computing setups, making it a vital tool in the modern data stack.

In the realm of data engineering - just like in software engineering, **reliable and efficient software is crucial**. Testing ensures reliability, maintainability, and efficiency of code. Given PySpark's role in extensive data transformations and analyses, however, testing is not straightforward.

As part of one of my own projects I dove deep into the best practices surrounding unit testing in data applications. Here, I'll go over the **benefits and principles of unit testing**, and how I approached **testing PySpark applications using Python's `pytest`**.

Any code used and the full example can be found on [GitHub](https://github.com/luijkr/unit-testing-pyspark/){:target="_blank"}.
{:.note}

# Basic Principles of Unit Testing

Unit testing in (PySpark) applications involves verifying the behavior of individual units. These units are typically functions or methods responsible for data transformations within the application. These units are fundamental building blocks critical to the overall functionality of the application. Adherence to key principles is paramount to ensure effective testing and maintain the robustness of these units and thus the codebase.

### 1. Isolation

Each unit test should be independently and **isolated from external factors**, such as other tests or the environment. Isolating tests **prevents unintended interactions** between them, ensuring that the outcome of a specific test remains consistent regardless of the order of execution or the context in which it is run.

### 2. Repeatable

Unit tests must **produce the same result each time they are executed**. Reproducibility is essential for identifying and diagnosing issues accurately. A repeatable test guarantees that the testing process is predictable, enabling developers to confidently detect any deviations in behavior and trace the source of discrepancies.

### 3. Fast

Efficient and swift execution of unit tests is crucial to maintain a **rapid development pace**. Slow tests can hinder productivity and deter developers from running them frequently.

### 4. Focused

Each unit test should concentrate on **evaluating a specific unit or a specific aspect of the code**. By maintaining a focused approach, tests become more targeted and easier to manage. Focused tests are instrumental in identifying the precise location of defects or areas requiring improvement, streamlining debugging efforts and enhancing code quality.

## Challenges in Unit Testing for (PySpark) Data Applications

Unit testing data-intensive applications poses unique challenges due to the volume and complexity of data being processed. Let's go over a few such challenges and how to approach these.

1. **Data Volume and Diversity:**

   - **Challenge:** Data-intensive applications often deal with large and diverse datasets, making it difficult to cover all possible data variations in unit tests.
   - **Solution:** Use representative samples, generate synthetic data, or utilize mocking frameworks to simulate various data scenarios.

2. **Data Dependency and Integration:**

   - **Challenge:** Data-centric applications often depend on external data sources, databases, APIs, or services, making it challenging to isolate and mock these dependencies for unit tests.
   - **Solution:** Use dependency injection, mocks, or stubs to simulate interactions with external data sources, ensuring tests remain focused and isolated.

3. **Data Transformation Logic:**

   - **Challenge:** Testing data transformation logic in isolation can be complex, especially when transformations involve intricate business rules or complex algorithms.
   - **Solution:** Break down transformation logic into smaller, testable units and design tests that validate the correctness of these units individually and in combination.

4. **Performance Impact of Testing:**

   - **Challenge:** Testing large volumes of data can significantly impact test execution time, hindering rapid feedback and iterative development.
   - **Solution:** Use appropriate data sampling or reduce dataset sizes for performance-focused unit tests, while also employing other types of tests (_e.g._, integration, end-to-end) to validate overall performance.

5. **Data Privacy and Security:**

   - **Challenge:** Data privacy and security concerns may restrict the usage of real data for testing purposes, making it challenging to create meaningful and compliant test scenarios.
   - **Solution:** Anonymize or pseudonymize sensitive data while preserving its essential characteristics to maintain privacy compliance during testing.

6. **Versioning and Schema Evolution:**

   - **Challenge:** Data-intensive applications often need to handle changes in data schemas or versions, making it crucial to ensure that tests are resilient to such changes.
   - **Solution:** Design tests to accommodate schema evolution by employing versioned or flexible data representations, enabling seamless adaptation to schema changes.

7. **Data Inconsistencies and Variability:**
   - **Challenge:** Real-world data often contains inconsistencies, missing values, or unexpected formats, making it difficult to create tests that cover all potential data scenarios.
   - **Solution:** Design tests that account for data inconsistencies and variability, considering edge cases and handling unexpected data gracefully within the application.

Addressing these challenges effectively is difficult. However, through thoughtful test design, appropriate testing strategies, and the use of specialized testing tools one should be able to enhance the reliability and effectiveness of unit testing in data-intensive applications.

# Example using pytest

In this section, we will go over a step-by-step example of writing unit tests for a PySpark application using `pytest`, a popular testing framework in Python. This framework allows the user to set up test fixtures and data, test the PySpark function with various input scenarios, and assert the expected outcomes. The full code can be found on [GitHub](https://github.com/luijkr/unit-testing-pyspark/){:target="_blank"}.

### NYC Taxi Dataset

In this example, we'll use the NYC Taxi dataset. This dataset consists of taxi rides in New York City. The data is stored in a simple CSV file.

### DataLoader

Let's consider a straightforward class called `DataLoader`, which only has one method that loads in the data from a CSV file.

{% gist 21c1830b42587ff0b8b549623b3bd916 data_loader.py %}

### DataTransformer

Next, let's define a `DataTransformer` class that has a single method to perform several simple transformations.

{% gist 21c1830b42587ff0b8b549623b3bd916 data_transformer.py %}

### Writing Unit Tests using pytest

Now, let's proceed with writing unit tests to ensure the correctness of the methods defined in these two classes. We will follow a structured approach:

#### Setting up Test Fixtures and Data

We start by setting up the necessary test fixtures and data. Note that when using `pytest`, you could define these fixtures in a `conftest.py` file, automatically making them availble in your tests.

First, we'll create a `spark` fixture, representing a `SparkSession`.

{% gist 21c1830b42587ff0b8b549623b3bd916 spark_fixture.py %}

Next, let's define a PySpark `DataFrame` with sample data to test the `test_transform_to_year_month` method.

{% gist 21c1830b42587ff0b8b549623b3bd916 sample_data_fixture.py %}

#### Testing the Various Methods

We will now write tests to validate the methods defined in the `DataLoader` and `DataTransformer` classes. Note that there is a single class corresponding to each of our original classes. _E.g.,_ for our `DataLoader` class we'll define a class with tests named `TestDataReader`.

{% gist 21c1830b42587ff0b8b549623b3bd916 test_data_reader.py %}

In our test, we check if the right number of rows are read. Of course, this test is a very simple and would not suffice in a real-world application. You would probably want to check other things, like the `DataFrame`'s schema.

Likewise, we can create a separate class with our tests for the `DataTransformer` class. This test will check if the right number of rows still exist in the returned `DataFrame`. In addition, we check whether the `year` and `month` columns are created and contain the expected values. Remember that we use the `sample_data` fixture we defined ourselves, so we know which values are expected to be returned by the `transform_to_year_month` method.

{% gist 21c1830b42587ff0b8b549623b3bd916 test_data_transformer.py %}

#### Running the Tests

To run all tests, simply execute the following command in your terminal:

```bash
pytest
```

A special `pytest.ini` file will list which directories for `pytest` to scan for tests.

{% gist 21c1830b42587ff0b8b549623b3bd916 pytest.ini %}

# Conclusion

In summary, unit testing is indispensable in testing any application, including PySpark applications. It offers a systematic and efficient way to ensure code reliability, maintainability, and correctness. Do note, however, that unit testing should be **one of several parts** of your testing suite. Always make sure to include other, higher-level tests as well, such as **integration tests** and even **end-to-end tests**.

The domain of PySpark testing introduces specific challenges and considerations when designing and implementing unit tests, distinct from conventional software engineering. Managing data dependencies, and handling large-scale and varied datasets necessitate tailored testing approaches.