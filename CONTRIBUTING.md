Getting Started
===================


## Clone repository:
> https://github.com/harijayms/terraform

## Create Azure SPN:
> See:
- https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli
- https://github.com/Azure/azure-devops-utils/blob/master/bash/create-service-principal.sh

## Configure local workstation for Terraform’s AzureRM provider, targeting an Azure subscription.


For each quickstart template:
-------------

## Create a branch resembling the name of the relevant azure quickstart template:

> **For example:**
>- **101-vm-simple-linux**, or
>- **topic/101-vm-simple-linux** or
>- **feature/101-vm-simple-linux**,
>- etc.

## Setup our workspace:

> Update the .gitignore in the root terraform directory to exclude the .terraform directory and its contents.

> Within the examples folder, create a new directory resembling the naming convention of existing Terraform examples:
> - **azure-vm-simple-linux**,
> - etc.

## Navigate to this directory.

## Each workspace will likely contain the following notable files:

> **README.md** – leverage relevant portions of the existing README.md from the quickstart repository, add additional notes that specifically apply to this Terraform configuration
> **main.tf** – this is generally understood to be the main entry point to your Terraform configuration
> **outputs.tf** – this will contain information received from the APIs/providers to display to the user/operator from the applied configuration
> **variables.tf** – these define parameters that extend the configurations capabilities
> **.travis.yml** – this defines the CI build/deploy steps for travis-ci.org

## Implement the core resources from the quickstart template

Core should go into the main.tf, outputs that should reside in outputs.tf, and adding parameters to the variables.tf.

> - Each template will start with an azurerm_resource_group resource as the container for the template’s resources
- **armviz.io** - is a good resource to visualize an ARM template, some quickstart templates will have a visualize button, but you can also load any ARM template
- the existing **azuredeploy.json** file will identify parameters, outputs, etc. which should generally map to outputs/variables/etc.
*Try to maintain variable names where possible*
- Certain resources in the azurerm provider can offer some flexibility, for example:
-- Use **azurerm_virtual_network** and **azurerm_subnet** resources, or
-- Use **azurerm_virtual_network** has its own subnet properties

## These templates are not tracking any state, or long-lived infrastructure, so we can ignore the .terraform folder in our .gitignore
## Commit early, commit often
## Submit PRs to contribute back into master, tagging relevant reviewers
