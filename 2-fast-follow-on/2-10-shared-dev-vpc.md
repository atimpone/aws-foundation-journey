# Shared Development VPC

*...given the benefits of moving to a shared development VPC for use across development team AWS accounts and the relative ease by which it can be set up and managed, it makes sesne to consider this a fast follow-on capability...*

## Motivation

* The organization needs to manage and pay for only one set of common shared VPC resources for all development teams.
* Configuration of organization standard newtork services such as AWS VPC endpoints is easier to manage in a single VPC.
* Teams reuse centrally managed VPC resources for multiple development teams.
* Teams have inherent connectivity to other teams' services given that their in the same VPC.
* Teams cannot see and manage other teams' workloads even though they're sharing the same VPCs.
* Teams cannot modify the VPC and related resources that are centally hosted and managed in a separate network AWS account.
* Costs for teams' cloud resources are still allocated to their respective development team AWS accounts.
* Costs for shared VPC foundation resources are allocated to the network AWS account.
