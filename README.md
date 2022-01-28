# composite-action-login-google

This repository stores a [composite action](https://github.blog/changelog/2021-08-25-github-actions-reduce-duplication-with-action-composition/) used to set up Google Cloud Platform (GCP) login in order to release a helm chart using helmfile. 

This means the action has to log into artifact registry as well as set up kubernetes context

You can use this composite action as a step in your workflow like:
```
- id: google-login
  if: ${{ steps.set-cloud-info.outputs.result == 'google' }}
  uses: prefapp/composite-action-login-google@v1
  with:
    creds: ${{ env.GOOGLE_CREDENTIALS }}
    cluster-name: ${{ env.CLUSTER_NAME }}
    cluster-location: ${{ env.CLUSTER_LOCATION }}

# ${{ steps.google-login.outputs.helmfile-creds }}
```