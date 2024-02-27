---
layout: post
title: Docker, GitHub, Actions!
subtitle: CI/CD Using Docker and GitHub Actions
image: 
  path: /assets/img/blog/docker-github.webp
  srcset:
    1060w: /assets/img/blog/docker-github.webp
    530w:  /assets/img/blog/docker-github@0,5x.webp
    265w:  /assets/img/blog/docker-github@0,25x.webp
hide_last_modified: true
---

In modern software development, Continuous Integration and Continuous Deployment ([CI/CD](https://resources.github.com/ci-cd/){:target="_blank"}) are **crucial for efficient, reliable, but above all _automated_ software delivery**. No one wants to _manually_ go through the process of testing your code (see [this post](/_posts/unit-testing-pyspark.markdown){:target="_blank"}) and deploying it. That's what CI/CD pipelines are for, allowing teams to release quality software at a rapid pace.

**Numerous services and tools** are available to facilitate such integration and deployment processes. Whatever your service of choice, they all require the user to define a pipeline. **This pipeline is run in some environment**. For example, in GitHub Actions you can specify the operating system using the `runs-on` parameter. The environment in which your pipeline runs, however, may not always what you want or need. For some applications, we want granular control over the _exact_ environment in which we run our CI/CD pipeline.

But if we can already specify the desired operating system, and if we can just install our dependencies on there, **why do we need Docker?**

## Why Use Docker?

Good question. Let's dive into some reasons why you might choose to use a Docker container instead of only choosing some operating system using the `runs-on` parameter provided by GitHub Actions.

**1. Application Isolation:** By using a Docker container, you can isolate your application and its dependencies from the host system and other actions in the workflow. This ensures that the workflow runs consistently regardless of the host environment.

**2. Environment Consistency:** Docker containers provide a consistent and reproducible environment. This is particularly useful when your application requires specific versions of libraries, tools, or dependencies to function correctly.

**3. Portability:** Docker containers are portable and can be easily moved and executed in different environments and operating systems that support Docker, making it easier to run the same workflow across various systems.

**4. Reuse and Sharing:** You can reuse existing Docker containers or share your custom Docker images with the community (_e.g.,_ through [Docker Hub](https://hub.docker.com/){:target="_blank"}), making it easier for others to use and contribute to your workflows.

**5. Version Control:** Docker images can be version-controlled, allowing you to track changes to the environment setup and easily roll back to previous versions if needed.

## Unit Testing a PySpark Application Using Docker and GitHub Actions

Now that we've got that out of the way, let's look at a simple CI/CD pipeline that aims to run unit tests for a PySpark project using Docker. Since we're using GitHub Actions, you can find this in the `.github` folder.

Any code used and the full example can be found in [GitHub](https://github.com/luijkr/unit-testing-pyspark/){:target="_blank"} in the `.github` folder. This repos contains a very basic pipeline using PySpark.
{:.note}

**First, we have to create an image.** To achieve this, a Dockerfile is needed that specifies what goes into this image. The image then serves as a blueprint for a container. But what should we include?

### Elements to Include in a Docker Container

When creating a Docker container for any project, it's essential (or at least advised) to **include several elements:**

1. **Base Image**: Choose a suitable base image (_e.g.,_ a specific version of Ubuntu) that provides the foundational operating system for your container.

2. **Dependencies**: Install the necessary dependencies for your project, such as Python (although base images with Python already available exist), pip, and any other libraries or tools required to run your application.

3. **Project Files**: Copy your project files from your local filesystem into the container, ensuring that the necessary scripts, configurations, and data are available within the container.

4. **Environment Configuration**: Set environment variables to configure your application. This could include environmental variables, authentication details, or any other environment-specific configurations.

5. **Execution Command**: Define the command to execute your application within the Docker container. This command should trigger the appropriate scripts or processes to run your project.

{:.note title="on base images"}
**Choose wisely.** Go with an official image whenever possible, and one that is as small as possible for your goal in order to avoid creating excessively large images.

### Dockerfile

With that in mind, let's go over the `Dockerfile` for the aforementioned PySpark application.

```Dockerfile
FROM ubuntu:latest

# Install required dependencies for your project
RUN apt-get update && apt-get install -y \
    python3.10 \
    pip \
    openjdk-8-jdk

# Copy your project files into the container
COPY . /

# Install Python requirements
RUN pip install -r requirements.txt

# Run the unit tests by invoking pytest
CMD ["pytest"]
```


**What does this Dockerfile do?**

- It specifies the base image for the Docker container. In this case, it's using the latest version of the Ubuntu image.
- Installs Python 3.10, the package manager `pip`, and the OpenJDK (Open Java Development Kit), which is necessary to run (Py)Spark.
- Copies the local project files (in the current directory) into the root folder `/` in the Docker container.
- Installs the requirements for the PySpark application, listed in `requirements.txt`.
- Defines the default command to be executed when the container is run. It will run `pytest`, which will trigger running all unit tests in the project.

### CI/CD Pipeline Using GitHub Actions

Without further ado, below is the workflow for GitHub Actions, and here's the [resulting run on GitHub](https://github.com/luijkr/unit-testing-pyspark/actions/runs/6970322035){:target="_blank"}.

```yaml
name: GitHub Actions for PySpark

run-name: GitHub Actions for Unit Testing PySpark

on: [push]

jobs:
  test-pyspark-applicaiton:
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository code
        uses: actions/checkout@v4
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."

      - name: Run tests in Docker container
        uses: docker://luijkr/unittestingpyspark:latest
        with:
          platforms: linux/amd64
```

Here's a breakdown of the steps:

1. **Check out repository code:**

- The workflow checks out the code from the repository using the `actions/checkout` action. This step ensures that the workflow has access to the latest version of the code.

2. **Run tests in Docker container:**

- This step uses a Docker container (`docker://luijkr/unittestingpyspark:latest`) to execute the PySpark tests.
- The `with` block specifies additional configuration options:
- `platforms: linux/amd64`: This sets the platform for the Docker container to Linux on the AMD64 architecture.

Overall, the workflow clones the repository, echoes a message to indicate successful code checkout, and then runs PySpark tests within a Docker container.

## Conclusion

Integrating Docker containers into your CI/CD workflow can significantly streamline and enhance the efficiency of your software development and deployment processes. Many flavors exist when it comes to places where your CI/CD pipelines can run. Here I used GitHub Actions as that is freely available to everyone.
