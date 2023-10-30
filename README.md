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

## How Azure Pipelines works?

The [Azure Pipelines](https://azure.microsoft.com/en-us/products/devops/pipelines) service
is very similar to GitHub Actions. You setup YAML files that describes a list of actions, or, pipelines to
be triggered whenever changes are pushed to your repository.

In GitHub Actions, you store these YAML files inside a `.github` folder in the root of
your project. But Azure Pipelines uses a single YAML file, which by default is named
as `azure-pipelines.yml` in the root of your project.

So everytime you see a `azure-pipelines.yml` file in the root of your project,
you know that it is a YAML that describes a pipeline, or a sequence of actions that
will be triggered when new changes are pushed to your repository.

## Which types of Quarto outputs this `azure-pipelines.yml` file supports

For the moment, the `azure-pipelines.yml` file in this repository can
only support compilation of Quarto projects to HTML output, and using Python only.
No R is supported yet.

## How the `azure-pipelines.yml` file in this repository works?

The `azure-pipelines.yml` file present in this repository performs the following steps:

1. Create a Azure Agent using the latest Ubuntu environment available at Azure.
1. Setup a new Python environment inside this Agent.
1. Copy the repository to this Agent environment (i.e. performs a `git clone` like action).
1. Downloads the latest release of Quarto at [quarto-dev/quarto-cli](https://github.com/quarto-dev/quarto-cli).
1. Installs the downloaded release of Quarto.
1. Runs the `quarto render` command over the repository.
1. Publishs the output/website to [Azure Static Web Apps](https://azure.microsoft.com/en-us/products/app-service/static).