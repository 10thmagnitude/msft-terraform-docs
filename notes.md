# BLOCKED ITEMS

## [201-vmss-ubuntu-autoscale](https://github.com/harijayms/terraform/tree/topic-201-vmss-ubuntu-autoscale/examples/azure-vmss-ubuntu-autoscale)
Blocker:
The AQS ARM requires that you create Auto Scale Settings, and there is currently not a resource for this within Terraform. 
- There is currently a [feature request](https://github.com/hashicorp/terraform/issues/12889) for Auto Scale Settings. 
- https://github.com/harijayms/terraform/tree/topic-201-vmss-ubuntu-autoscale

The current example that is committed to this [topic branch](https://github.com/harijayms/terraform/tree/topic-201-vmss-ubuntu-autoscale/examples/azure-vmss-ubuntu-autoscale) provisions everything else that this ARM requires but leaves the auto-scaling commented out.

A template was created in its place that leaves out the auto-scaling and is called [azure-vmss-ubuntu](https://github.com/hashicorp/terraform/pull/15290), and it is currently in Hashicorp PR review.

## [201-web-app-redis-cache-sql-database](https://github.com/harijayms/terraform/tree/topic-201-web-app-redis-cache-sql-database/examples/azure-web-app-redis-cache-sql-database)
This template is blocked by two resources that Terraform currently lacks:
1. Web/sites
2. Web/serverfarms

There is currently a [feature request](https://github.com/hashicorp/terraform/pull/12001) that is in progress for these resources, but no progress has been made on it in about a month.

# CI CLEANUP

After the final two templates get pulled into Hashicorp's master (openshift and vmss), then I will submit one final pull request to Hashicorp to clean up some of our deploy scripts with new environment variables and other misc clean up. These changes do not affect whether the templates will work or not, only whether they work properly in the Travis CI that we have set up in your subscription. 

> Edited to add: Now that all of the example templates are merged into Hashicorp's master branch, I have submitted a final PR for the `hashicorp-ci-updates` branch. The branch that will be left on Hari's fork is called `topic-ci-updates`, and it contains the latest and most accurate version of the `.travis.yml`. [![Build Status](https://travis-ci.org/harijayms/terraform.svg?branch=topic-ci-updates)](https://travis-ci.org/harijayms/terraform)