---
title: "Azure DevOps Build Pipeline"
date: 2020-11-15T19:45:09Z
draft: false
---
# Azure DevOps Build Pipeline

## [Overview](https://docs.microsoft.com/en-us/azure/devops/pipelines/get-started/key-pipelines-concepts?view=azure-devops)

![](.gitbook/assets/image%20%2818%29.png)

* A trigger tells a Pipeline to run
* A pipeline is made of one or more stages. A pipeline can deploy to one or more environments
* A stage is a way of organizing jobs in a pipeline and each stage can have one more jobs
* Each job runs on one agent. A job can also be agentless
* Each agent runs a job that contains one or more steps
* A step can be a task or script and is the smallest building block of a pipeline.
* As task is a pre-packged script that performs an action, such as invoking a REST API or publishing a build artifact.
* An artifact is a collection of files or packages published by a run.



