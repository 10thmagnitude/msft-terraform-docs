Getting Started
===================

## Clone this fork of the Terraform repository:
 https://github.com/harijayms/terraform

## Create Azure SPN:
See:
 - https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli
 - https://github.com/Azure/azure-devops-utils/blob/master/bash/create-service-principal.sh

## Configure local workstation for Terraform’s AzureRM provider, targeting an Azure subscription.

For each Quickstart template:
-------------

## Create a branch resembling the name of the relevant [Azure Quickstart Template](https://github.com/Azure/azure-quickstart-templates), prefixed with `topic-`:

> **For example:**
>- `topic-101-vm-simple-linux`

## Setup your workspace:

 Update the `.gitignore` in the root Terraform directory to exclude the following:

 ```
 terraform.tfvars
*.tfstate*
.gitignore
out.*
```

Within the `examples` folder, create a new directory resembling the naming convention of existing Terraform examples, for example `azure-vm-simple-linux`.

## Each workspace will likely contain the following notable files:

 - `README.md` – Leverage relevant portions of the existing README.md from the Quickstart repository, and add additional notes that specifically apply to this Terraform configuration.
 - `main.tf` – This is generally understood to be the main entry point to your Terraform configuration.
 - `outputs.tf` – This will contain information received from the APIs/providers to display to the user/operator from the applied configuration.
 - `variables.tf` – These define parameters that extend the configurations capabilities.
 - `deploy.ci.sh` - This is the script consumed by travis-ci for CI.
 - `deploy.mac.sh` - This is the wrapper around `deploy.ci.sh` for testing on your local workstation (tested on macOS 10.12.4).

## Implement the core resources from the Quickstart template

Core should go into the `main.tf`, outputs that should reside in `outputs.tf`, and adding parameters to the `variables.tf`.

- Each template will start with an `azurerm_resource_group` resource as the container for the template’s resources.
- **armviz.io** - is a good resource to visualize an ARM template, some quickstart templates will have a visualize button, but you can also load any ARM template
- the existing **azuredeploy.json** file will identify parameters, outputs, etc. which should generally map to outputs/variables/etc.
- Try to maintain variable names where possible, however switch to snake casing instead of camel casing.
- Certain resources in the azurerm provider can offer some flexibility, for example:
-- Use `azurerm_virtual_network` and `azurerm_subnet` resources, or
-- Use `azurerm_virtual_network` has its own subnet properties

_**These templates are not tracking any state, or long-lived infrastructure, so we can ignore the .terraform folder in our .gitignore**_

_**Commit early, commit often**_

_**Submit PRs to contribute back into master, tagging relevant reviewers**_

_**Continuous Integration with travis-ci**_
> - `See CI.md`

## MORE TIPS FOR USING TERRAFORM WITH AZURE
- It is nice to be able to add the **Subnet** as a nested resource within the VNET resource, however, there are many times in which you have to reference the Subnet ID, and you cannot do this when it is nested; the Subnet must be a freestanding resource in order to reference its ID.

- The best way in which to run any process on a machine at the time of provisioning is by using an `azurerm_virtual_machine_extension`. [The extension resource](https://www.terraform.io/docs/providers/azurerm/r/virtual_machine_extension.html) is simplest and preferred as it allows for the process to be done with root privileges without the need to provide any sort of credentials. 

- If you would like to create a graph of the template that you created, you may run this command from within your template's directory:

```
terraform graph | dot -Tpng > graph.png
```
