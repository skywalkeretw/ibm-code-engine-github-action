# Code Engine Deploy GitHub Action

This GitHub Action, named "Code Engine Deploy," facilitates the deployment of Apps, Functions, and Jobs to IBM Cloud Code Engine.

## Author
- Author: Skywalker_etw

## Description
This action allows you to deploy Apps, Functions, and Jobs to IBM Cloud Code Engine. It offers flexibility for different deployment types, and you can configure it with the following inputs:

- `api-key` (required): IAM API Key used to log into the IBM Cloud. Please note that you should store your IBM Cloud API key securely in your GitHub repository secrets..
- `resouce-groupe` (optional, default: Default): An IBM Cloud Resource Group, a logical container for organizing and managing related cloud resources.
- `region` (required): The geographical area where your Code Engine project is located.
- `project` (required): A Code Engine Project, grouping your Apps, Functions, and Jobs.
- `entity` (required): The type of entity to deploy (App, Function, Job).
- `name` (required): The name of the App, Function, or Job.
- `runtime` (required for Function): The runtime used for the Function.
- `build-source` (optional, default: .): Path to the directory containing the source code.

## Usage
To use this action, add it to your GitHub Actions workflow YAML file. For example:

```yaml
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
      uses: Skywalker_etw/code-engine-deploy-action@betav1
      with:
        api-key: ${{ secrets.IBM_CLOUD_API_KEY }}
        resouce-groupe: 'Default'
        region: 'us-south'
        project: 'my-code-engine-project'
        entity: 'app'
        name: 'my-app-name'
        build-source: 'path/to/source'
```

This action is not officially endorsed by IBM Cloud but can be used as a community-contributed GitHub Action.
