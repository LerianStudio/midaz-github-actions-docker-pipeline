# Midaz GitHub Actions docker pipeline

### GitHub Action: Docker Build, AWS ECR Push and Kustomize step

This GitHub Action module automates the process of building a Docker image, pushing it to an AWS container registry (such as Amazon Elastic Container Registry - ECR), and running Kustomize steps for Kubernetes deployment.

## Inputs

- **app-name:** 'The app name'
- **argo-cd-sync:** 'Do you want to run the ArgoCD sync for this application in DEV environment?'
- **argo-cd-token:** 'The ArgoCD token to sync after Kustomize step'
- **argo-cd-url:** 'The ArgoCD URL to be used in application sync step'
- **aws-region:** 'AWS region name to assume role'
- **dockerfile-name:** 'The Dockerfile name'
- **k8s-manifest-repo-name:** 'The name of K8S manifests repository'
- **k8s-manifest-repo-url:** 'The URL of K8S manifests repository'
- **role-session-name:** 'The AWS Session name'
- **role-to-assume:** 'The AWS OICD role to assume'
- **service-github-token:** 'The service user token on Git Hub'
- **slack-webhook-url:** 'The webhook URL to send notifications to slack'

**OBS.:** All inputs are **required**

## Outputs

There are no outputs for this action

## Example usage

```yaml
    on: [push]

    permissions:
      id-token: write # This is required for aws oidc connection
      contents: read # This is required for actions/checkout
      pull-requests: write # This is required for gh bot to comment PR

    jobs:
      go_pipeline:
        runs-on: ubuntu-latest
        name: Go lang pipeline
        steps:
          - uses: actions/checkout@v3
            uses: <ORG NAME>/github-actions-go-pipeline-template@main
            with:
              app-name: '<to fill>'
              argo-cd-sync: '<to fill>'
              argo-cd-token: '<to fill>'
              argo-cd-url: '<to fill>'
              aws-region: '<to fill>'
              dockerfile-name: '<to fill>'
              k8s-manifest-repo-name: '<to fill>'
              k8s-manifest-repo-url: '<to fill>'
              role-session-name: '<to fill>'
              role-to-assume: '<to fill>'
              service-github-token: '<to fill>'
              slack-webhook-url: '<to fill>'
```

## How to send updates?
If you wants to update or make changes in module code you should use the **develop** branch of this repository, you can test your module changes passing the `@develop` in module calling. Ex.:

```yaml
    on: [push]

    permissions:
      id-token: write # This is required for aws oidc connection
      contents: read # This is required for actions/checkout
      pull-requests: write # This is required for gh bot to comment PR

    jobs:
      go_pipeline:
        runs-on: ubuntu-latest
        name: Go lang pipeline
        steps:
          - uses: actions/checkout@v3
            uses: <ORG NAME>/github-actions-go-pipeline-template@develop
            with:
              app-name: '<to fill>'
              argo-cd-sync: '<to fill>'
              argo-cd-token: '<to fill>'
              argo-cd-url: '<to fill>'
              aws-region: '<to fill>'
              dockerfile-name: '<to fill>'
              k8s-manifest-repo-name: '<to fill>'
              k8s-manifest-repo-url: '<to fill>'
              role-session-name: '<to fill>'
              role-to-assume: '<to fill>'
              service-github-token: '<to fill>'
              slack-webhook-url: '<to fill>'
```
After execute all tests you can open a pull request to the main branch.