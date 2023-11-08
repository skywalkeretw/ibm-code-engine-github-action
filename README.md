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
- `memory` (optional): Memory used for your App, Function, or Job, default is the value as described in the Code Engine Docs.
- `cpu` (optional): CPU used for your App, Function, or Job, default is the value as described in the Code Engine Docs.

Additionally, this action provides options for creating and updating ConfigMaps with the following input parameters:

- `configmap` (optional): The name of the ConfigMap to create or update.
- `configmap-env-file` (optional): Specify the path to a file or files to read lines of key=val pairs for the ConfigMap.
- `configmap-file` (optional): Set a key from a file. The format must be FILE or KEY=/path/to/file.
- `configmap-literal` (optional): Set key-value pairs for the ConfigMap.

The action handles the creation and updating of ConfigMaps based on the provided input parameters. It checks if any of the `configmap-env-file`, `configmap-file`, or `configmap-literal` inputs are set. If any of these inputs are set, it constructs the appropriate `--from-env-file`, `--from-file`, or `--from-literal` arguments for creating or updating the ConfigMap.

The action checks if the ConfigMap with the provided name already exists. If it exists, it updates the ConfigMap; otherwise, it creates a new one.



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
      uses: Skywalker_etw/code-engine-deploy-action@v1
      with:
        api-key: ${{ secrets.IBM_CLOUD_API_KEY }}
        resouce-groupe: 'Default'
        region: 'us-south'
        project: 'my-code-engine-project'
        entity: 'app'
        name: 'my-app-name'
        build-source: 'path/to/source'
```

Here is also an example how to create a configmap. `configmap-env-file`, `configmap-file` and `configmap-literal` can all take multiple values  using the described notation in the example
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
      uses: Skywalker_etw/code-engine-deploy-action@v1
      with:
        api-key: ${{ secrets.IBM_CLOUD_API_KEY }}
        resouce-groupe: 'Default'
        region: 'us-south'
        project: 'my-code-engine-project'
        entity: 'app'
        name: 'my-app-name'
        build-source: 'path/to/source'
        configmap: |
                'my-key-1=my-value-1'
                'my-key-2=my-value-2'
```

```yml
name: Deploy to Code Engine
on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@v2

    - name: Deploy to Code Engine
      uses: your-username/code-engine-deploy-action@v1
      with:
        api-key: ${{ secrets.IBM_CLOUD_API_KEY }}
        resource-group: 'Default'
        region: 'us-south'
        project: 'my-project'
        entity: 'app'
        name: 'my-app'
        runtime: 'nodejs'
        build-source: './app-source'
        memory: '256Mi'
        cpu: '0.25'
        configmap: 'my-configmap'
        configmap-env-file: ./config.env
        configmap-file: file-key=./path/to/file
        configmap-literal: |
                        key1=value1
                        key2=value2
```
This action is not officially endorsed by IBM Cloud but can be used as a community-contributed GitHub Action.
