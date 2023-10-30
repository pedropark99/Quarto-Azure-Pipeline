# Quarto-Azure-Pipeline

If your organization uses Azure DevOps instead of GitHub for storing repositories,
you might need to setup a CI pipeline for automatically build and publish Quarto projects
using the Azure tools.

This repository stores an `azure-pipelines.yml` example that you can use to setup a simple
CI pipeline for your Quarto projects hosted on Azure DevOps, using
[Azure Pipelines](https://azure.microsoft.com/en-us/products/devops/pipelines)
and [Azure Static Web Apps](https://azure.microsoft.com/en-us/products/app-service/static).

Basically, all you need is to create a new [PAT (Personal Access Token) in Azure](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=Windows)
and use this new PAT you created inside the YAML, at the `azure_static_web_apps_api_token` step.
