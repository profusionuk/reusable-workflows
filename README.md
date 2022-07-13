<h2 align="center">
Reusable GitHub actions
</h2>

<div align="center">
  Common and useful GitHub actions
</div>

This is a collection of **GitHub Actions** to deploy your commonly reusable workflows in a version controlled state.


For new users of GitHub Actions:
Note that the `GITHUB_TOKEN` is **NOT** a personal access token.
A GitHub Actions runner automatically creates a `GITHUB_TOKEN` secret to authenticate in your workflow.
So, you can start to deploy immediately without any configuration.

## Table of Contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Table of Contents](#table-of-contents)
- [Getting started](#getting-started)
- [Examples](#examples)
  - [⭐️ Python Pytest](#️-python-pytest)
  - [⭐️ Terraform AWS apply](#️-terraform-aws-apply)
  - [⭐️ Deploy Docker image to AWS ECR](#️-deploy-docker-image-to-aws-ecr)
  - [⭐️ Run Serverless Deploy with assume-roles](#️-run-serverless-deploy-with-assume-roles)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->



## Getting started

Fork this repository into your own account, and start deploying your workflows using the below examples.

## Examples

### ⭐️ Python Pytest

This is an example workflow for Python Pytest.
This workflow will take a Python version as an input, pip install your requirements.txt file, and run your tests.

```yaml
# The name of the action
name: 'Python Tests'

# Paths: will run tests only if code in the given directory changes
on:
  push:
    branches:
      - main
    paths:
      - "*/*.py"
      - "*.py"


# What to do when the action is triggered
jobs:
  pytest:
    name: "Python tests"
    uses: "YOUR-USER/YOUR-REPOSITORY-NAME/.github/workflows/python-pytest.yml@main"
    with:
    # The Python version your code is written in
      python-version: "3.9.1"
```

<div align="right">
<a href="#table-of-contents">Back to TOC</a>
</div>


### ⭐️ Python Pytest with Coverage

This is an example workflow for Python Pytest and a coverage report posted on PR.
This workflow will take a Python version as an input, pip install your requirements.txt file, run your tests and export a code coverage report to a PR comment.

```yaml
# The name of the action
name: 'Python Tests with Coverage'

# Paths: will run tests only if code in the given directory changes
on:
  push:
    branches:
      - main
    paths:
      - "*/*.py"
      - "*.py"


# What to do when the action is triggered
jobs:
  pytest:
    name: "Python tests"
    uses: "YOUR-USER/YOUR-REPOSITORY-NAME/.github/workflows/python-pytest-with-coverage.yml@main"
    with:
    # The Python version your code is written in
      python-version: "3.9.1"
```

<div align="right">
<a href="#table-of-contents">Back to TOC</a>
</div>


### ⭐️ Terraform AWS apply

This is an example workflow for Terraform deployments.
This workflow will take an AWS access key and secret key as an input, and apply your Terraform configuration.

```yaml
# The name of the action
name: 'Terraform'

# Paths: will run tests only if code in the given directory changes
on:
  push:
    branches:
      - main
    paths:
      - "*/*.tf"


# What to do when the action is triggered
jobs:
  terraform:
    name: "Terraform"
    uses: "YOUR-USER/YOUR-REPOSITORY-NAME/.github/workflows/terraform-deploy.yml@main"
    secrets:
      aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

<div align="right">
<a href="#table-of-contents">Back to TOC</a>
</div>


### ⭐️ Deploy Docker image to AWS ECR

This is an example workflow for building Docker images, and deploying them to Elastic Container Registry.
This workflow will take an AWS access key, secret key, region, repository name and IAM role to assume into as an input.

```yaml
# The name of the action
name: 'Docker deploy'

# Paths: will run tests only if code in the given directory changes
on:
  push:
    branches:
      - main


# What to do when the action is triggered
jobs:
  # Build the docker image, tag it, and push it to ECR
  deploy:
    name: Deploy
    # Create dependancy job on successful testing
    uses: "YOUR-USER/YOUR-REPOSITORY-NAME/.github/workflows/build-and-push-docker-ecr.yml@main"
    with:
      aws-region: "AWS-REGION"
      repo-name: "ECR-REPOSITORY-NAME"
      role-to-assume: "IAM-ROLE-ARN"
    secrets:
      aws-access-key-id: ${{secrets.AWS_ACCESS_KEY_ID}}
      aws-secret-access-key: ${{secrets.AWS_SECRET_ACCESS_KEY}}

```

### ⭐️ Run Serverless Deploy with assume-roles

This is an example workflow for running serverless deploy assuming into another account.
This workflow will take an AWS access key, secret key, region, role-arn.

```yaml
# The name of the action
name: 'Serverless Deploy'

# Paths: will run tests only if code in the given directory changes
on:
  push:
    branches:
      - main


# What to do when the action is triggered
jobs:
  # Execure the serverless deploy job
  deploy:
    name: Deploy
    # Create deployment job
    uses: "YOUR-USER/YOUR-REPOSITORY-NAME/.github/workflows/serverless-deploy.yml@main"
    secrets:
      AWS_ACCESS_KEY_ID: ${{secrets.AWS_ACCESS_KEY_ID}}
      AWS_SECRET_ACCESS_KEY: ${{secrets.AWS_SECRET_ACCESS_KEY}}
      REGION: ${{secrets.AWS_REGION}}
      ROLE_ARN: ${{secrets.ROLE_ARN}}

```

<div align="right">
<a href="#table-of-contents">Back to TOC</a>
</div>
