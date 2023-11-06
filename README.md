# ibm-code-engine-github-action
Unofficial Github action for depolying to IBM Code Engine

## Usage

### Deploy a function
```yaml
- name: Deploy Function to IBM Cloud Code Engine
  uses: skywalkeretw/ibm-code-engine-github-action
  with:
    api-key: ${{ secrets.IBM_IAM_API_KEY }}
    region: eu-de
    project: my-project
    entity: function
    name: my-func
    runtime: nodejs
```
