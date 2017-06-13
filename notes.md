# BLOCKED ITEMS

## [201-vmss-ubuntu-autoscale](https://github.com/harijayms/terraform/tree/topic-201-vmss-ubuntu-autoscale/examples/azure-vmss-ubuntu-autoscale)
This template is blocked by two things:
1. The AQS ARM requires that you specify IDs for the `loadBalancerInboundNatPools` in the NIC configuration of the VM Scale Set, however Terraform does not currently have a resource for importing those IDs.
  - We have submitted an [issue](https://github.com/hashicorp/terraform/issues/13902) into Hashicorp requesting this functionality. 
2. The AQS ARM requires that you create Auto Scale Settings, and there is currently not a resource for this within Terraform. 
  - There is currently a [feature request](https://github.com/hashicorp/terraform/issues/12889) for Auto Scale Settings. 
- https://github.com/harijayms/terraform/tree/topic-201-vmss-ubuntu-autoscale

The current example that is committed to this [topic branch](https://github.com/harijayms/terraform/tree/topic-201-vmss-ubuntu-autoscale/examples/azure-vmss-ubuntu-autoscale) provisions everything else that this ARM requires but leaves those two blocked items commented out.

## [201-web-app-redis-cache-sql-database](https://github.com/harijayms/terraform/tree/topic-201-web-app-redis-cache-sql-database/examples/azure-web-app-redis-cache-sql-database)
This template is blocked by two resources that Terraform currently lacks:
1. Web/sites
2. Web/serverfarms

There is currently a [feature request](https://github.com/hashicorp/terraform/pull/12001) that is in progress for these resources, but no progress has been made on it in about a month.

