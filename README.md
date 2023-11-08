# Code Engine Deploy GitHub Action

This GitHub Action allows you to deploy Apps, Jobs, and Functions to IBM Cloud Code Engine. It offers flexibility for different deployment types and provides various configuration options. 

## Author
- Author: Skywalker_etw

## Description
This action allows you to deploy Apps, Functions, and Jobs to IBM Cloud Code Engine. It offers flexibility for different deployment types, and you can configure it with the following inputs:

### Inputs

- `api-key` (required): IAM API Key used to log into the IBM Cloud. Please store your IBM Cloud API key securely in your GitHub repository secrets.
- `resouce-groupe` (optional, default: Default): An IBM Cloud Resource Group, a logical container for organizing and managing related cloud resources.
- `region` (required): The geographical area where your Code Engine project is located.
- `project` (required): A Code Engine Project, grouping your Apps, Functions, and Jobs.
- `entity` (required): The type of entity to deploy (App, Function, Job).
- `name` (required): The name of the App, Function, or Job.
- `runtime` (required for Function): The runtime used for the Function. Currently supported `nodejs-18` and `python-3.11` see [IBM Code Engine Function Runtimes](https://cloud.ibm.com/docs/codeengine?topic=codeengine-fun-runtime) for more information.
- `build-source` (optional, default: .): Path to the directory containing the source code.



## Usage
To use this action, add it to your GitHub Actions workflow YAML file. For example:

```yaml
name: Deploy to Code Engine
on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    name: Deploy to Code Engine
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Deploy to Code Engine
      uses: skywalkeretw/ibm-code-engine-github-action@v1
      with:
        api-key: ${{ secrets.IBM_CLOUD_API_KEY }}
        region: 'us-south'
        project: 'my-code-engine-project'
        entity: 'app'
        name: 'my-app-name'
        build-source: 'path/to/source'
```

This action is not officially endorsed by IBM Cloud but can be used as a community-contributed GitHub Action.
