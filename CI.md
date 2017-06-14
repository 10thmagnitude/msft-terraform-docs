Getting Started with Continuous Integration for Terraform Examples
===================

**CI is handled via Travis-CI:  https://travis-ci.org/harijayms/terraform/branches.**

## About Travis-CI
Travis-CI is a build (and deployment) orchestration SaaS tool.

## Why Travis-CI?
Cost - Free for open-source projects

Ease of use

Extensibility

Key Features:
- Management interface for sensitive environment variables
- Multiple builds are capable of being executed in parallel with isolation by source branch, and directory

## Travis-CI basics:
Travis-CI provides us a set of pipeline steps that are configurable.

Travis-CI looks for a **.travis.yml** file in the root of the repository that allows us to configure what those steps do.

## How are we using Travis-CI for build/deploy?

Key pipeline steps that we are configuring are:
- **before_deploy**
This step will setup any environment variables consumed during our "build", validate, deploy, test process.

- **deploy**
This step will actually handle the deployment, testing, and destruction of resources managed by terraform.  

## When/where do Travis-CI builds run?
Travis-CI is configured to run on changes to:
- master
- branches with a prefix of "topic-" (this is open to change) on commit
- open of a pull request

## Where can I view the build history?
https://travis-ci.org/harijayms/terraform/branches

## How are secrets managed?
Travis-CI can securely store secrets as [Environment Variables](https://travis-ci.org/harijayms/terraform/settings) per repository, which are later configured on build agents.

The environment variables that are currently being stored in Travis for consumption by Terraform are:
- `ARM_CLIENT_ID`
- `ARM_CLIENT_SECRET`    
- `ARM_SUBSCRIPTION_ID`    
- `ARM_TENANT_ID`
- `KEY_ENCRYPTION_KEY_URL` 
- `KEY_VAULT_RESOURCE_ID`  
- `SSH_PUBLIC_KEY`

## How can Travis-CI do parallel builds?
We will leverage the Build Matrix feature to kick off CI of multiple examples on our master branch.

For example, the following will tell Travis-CI to kick off a job for each TEST_DIR and aggregate the results for a build:

```env:
  - TEST_DIR=examples/azure-vm-simple-linux-managed-disk
  - TEST_DIR=examples/azure-vm-from-user-image
```

### What is our pipeline's process at a high level?
Spin up a linux build agent in GCE

Pull source (git clone/checkout)

Setup env variables from repository settings

Setup env variables from .travis.yml

build/deploy/test/destroy
- `terraform get`
- `terraform validate`
- `terraform plan`
- `terraform apply`
- *Any additional testing via Azure CLI, etc.*
- `terraform destroy`

Tear down linux build agent

## Permanent Resource Group

This CI process depends on a resource group in your subscription called `permanent`. This resource group contains the following resources:

|Name             | ResourceGroup   | Location       | Type                                |
|---------------- | --------------- | -------------- | ----------------------------------- |
|LinuxImage       | permanent       | southcentralus | Microsoft.Compute/images            |
|WindowsImage     | permanent       | southcentralus | Microsoft.Compute/images            |
|TerraformVault   | permanent       | southcentralus | Microsoft.KeyVault/vaults           |
|permanent-vnet   | permanent       | southcentralus | Microsoft.Network/virtualNetworks   |
|tfpermstor       | permanent       | southcentralus | Microsoft.Storage/storageAccounts   |

_It is strongly suggested that you add locks to prevent these resources from being destroyed. For example: 

```
az lock create --name lockImage1ForCI --lock-type CanNotDelete -g permanent --resource-type Microsoft.Compute/images --resource-name LinuxImage
```