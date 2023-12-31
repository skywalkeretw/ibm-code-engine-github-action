# Code Engine Deploy GitHub Action

This GitHub Action allows you to deploy Apps, Jobs, and Functions to IBM Cloud Code Engine. It offers flexibility for different deployment types and provides various configuration options. 

## Author
- Author: Skywalker_etw

## Description
This action allows you to deploy Apps, Functions, and Jobs to IBM Cloud Code Engine. It offers flexibility for different deployment types, and you can configure it with the following inputs:

### Inputs

| Name            | Required | Default Value |Description |
|-----------------|----------|---------------|----------------------------------------------------------------|
| `api-key`       | ✅      | -             | IAM API Key used to log into the IBM Cloud. Please store your IBM Cloud API key securely in your GitHub repository Secrets.|
| `resource-group`| ❌       | Default       | An IBM Cloud Resource Group, a logical container for organizing and managing related cloud resources.|
| `region`        | ✅      | -             | The geographical area where your Code Engine project is located.|
| `project`       | ✅      | -             | A Code Engine Project, grouping your Apps, Functions, and Jobs.|
| `entity`        | ✅      | -             | The type of entity to deploy (App, Function, Job). |
| `name`          | ✅      | -             | The name of the App, Function, or Job.|
| `runtime`       | ❌ | -             | The runtime used for the Function. Currently supported `nodejs-18` and `python-3.11` see [IBM Code Engine Function Runtimes](https://cloud.ibm.com/docs/codeengine?topic=codeengine-fun-runtime) for more information.|
| `build-source`  | ❌       | .             | Path to the directory containing the source code.|
| `cpu`           | ❌       | -             | CPU value set for your entity [Config for Functions](https://cloud.ibm.com/docs/codeengine?topic=codeengine-fun-runtime), [Codeengine Memory CPU combo](https://cloud.ibm.com/docs/codeengine?topic=codeengine-mem-cpu-combo)|
| `memory`        | ❌       | -             | Memory value set for your entity [Config for Functions](https://cloud.ibm.com/docs/codeengine?topic=codeengine-fun-runtime), [Codeengine Memory CPU combo](https://cloud.ibm.com/docs/codeengine?topic=codeengine-mem-cpu-combo)|




## Usage
To use this action, add it to your GitHub Actions workflow YAML file. 
Has examples for Each function, app and job
For example:

```yaml
name: Depoly to Code Engine

on:
  push:
    branches:
      - master
      -

jobs:

  app:
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@v3

    - name: Deploy Application to Code Engine
      uses: skywalkeretw/ibm-code-engine-github-action@v1
      with:
        api-key: ${{ secrets.IBM_IAM_API_KEY }}
        resource-group: 'Default'
        region: 'eu-de'
        project: 'MY-PROJECT'
        entity: 'app'
        name: 'my-qpp'
        build-source: './app'
        cpu: 1
        memory: 4G

  job:
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@v3

    - name: Deploy Job to Code Engine
      uses: skywalkeretw/ibm-code-engine-github-action@v1
      with:
        api-key: ${{ secrets.IBM_IAM_API_KEY }}
        resource-group: 'Default'
        region: 'eu-de'
        project: 'MY-PROJECT'
        entity: 'job'
        name: 'my-job'
        build-source: './job'
        cpu: 1
        memory: 4G

  fn-js:
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@v3

    - name: Deploy JavaScript Function to Code Engine
      uses: skywalkeretw/ibm-code-engine-github-action@v1
      with:
        api-key: ${{ secrets.IBM_IAM_API_KEY }}
        resource-group: 'Default'
        region: 'eu-de'
        project: 'MY-PROJECT'
        entity: 'fn'
        runtime: nodejs-18 
        name: 'my-js-fn'
        build-source: './js-func'
        cpu: 1
        memory: 4G

  fn-py:
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@v3

    - name: Deploy Python Function to Code Engine
      uses: skywalkeretw/ibm-code-engine-github-action@v1
      with:
        api-key: ${{ secrets.IBM_IAM_API_KEY }}
        resource-group: 'Default'
        region: 'eu-de'
        project: 'MY-PROJECT'
        entity: 'fn'
        runtime: python-3.11
        name: 'my-py-fn'
        build-source: './py-func'
        cpu: 1
        memory: 4G
```

This action is not officially endorsed by IBM Cloud but can be used as a community-contributed GitHub Action.
