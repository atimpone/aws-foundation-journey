# Initial Development Environment Solution Overview

The following diagram represents a typical team development environment as a distinct AWS account supported by an initial set of foundation capabilities managed via a set of shared AWS accounts to meet the typical requirements outlined above. 

Since your specific requirements may include some of the optional [fast follow-on capabilities](../README.md#2-establish-fast-follow-on-capabilities), aspects of your initial solution may be different than shown in this diagram.

![alt text](https://github.com/ckamps/aws-foundation-journey/raw/master/images/dev-initial.png "Initial Development Environment")

Key aspects of the initial, minimal solution include:

## Initial Users of Your AWS Environment

The initial development team, your designated cloud administrators, security and compliance team members, and potentially your finance team members who are concerned with cloud spend, will typically use their corporate desktops to access the AWS Management Console and AWS service APIs over the Internet.

Technical users will typically install the AWS Command Line Interface (CLI) and related Software Development Kits (SDKs) on their local corporate desktops to ease the process of interacting with your AWS environment.

## Development Team AWS Accounts

Each development team is allocated a distinct AWS account to act as a resource container for the AWS resources a team creates and manages on its own.  Since AWS service costs are automatically reported for each AWS account, using a distinct AWS account for each team’s development needs is a convenient way to make costs visible and attributable to each team.

In addition to your initial application and data engineering development teams that need access to the AWS platform, you should view your initial cloud and security administrators as a development team in its own right that should have its own AWS account for its own work to iterate on, develop, and perform early testing of changes to the foundation..

## Shared Development VPC Network

A shared development network in the form of an AWS Virtual Private Cloud (VPC) will be used to support the networking needs of development teams.  Your Cloud Administrators will provision this shared development VPC to a new "Network" AWS account and share it with all future development team AWS accounts.

The shared VPC will support cases in which a development team needs to deploy AWS resources that reside in VPCs. For example, deploying Amazon EC2 Virtual Machines (VMs) and Amazon Relational Database Service (RDS) instances. The shared development VPC provides both public and private subnets across multiple Availability Zones (AZs) to both mimic typical production topologies and enable teams to access Internet-based resources such as package repositories and publicly available APIs during their experiment and development work.

Benefits of using a shared VPC for development team include:
* The organization needs to manage and pay for only one set of common shared VPC resources for all development teams. For example, one set of NAT Gateways - which are billed on an hourly basis.
* Configuration of organization standard newtork services such as AWS VPC endpoints is easier to manage in a single VPC.
* Development teams reuse centrally managed VPC resources for multiple development teams.
* Development teams still manage security groups, ec2 instances, etc.
* Development teams have inherent connectivity to other teams' services given that they are in the same VPC.
* Development teams cannot see and manage other teams' workloads even though they're sharing the same VPCs.
* Development teams cannot modify the VPC and related resources that are centally hosted and managed in a separate network AWS account. No additional IAM policies are required.
* Costs for development teams' cloud resources are still allocated to their respective development team AWS accounts.
* Costs for shared VPC foundation resources are allocated to the network AWS account.

## Direct Internet Access

In this initial stage of your foundation, your users’ existing access to the Internet via the corporate network is used both to enable all users to access the AWS platform and to enable developers to access their workloads and data services hosted in their development team AWS accounts.

In this initial stage, there’s no network connectivity between your AWS accounts and your on-premises data center.

## AWS Single Sign-On (SSO)

AWS SSO is used to manage the initial relatively limited number of human users across your development teams and cloud administrators who need to access the AWS Management Console and AWS APIs to get things done in either team development AWS accounts or in support of managing and operating the overall use of AWS. Initially, you’ll use a locally managed store of groups and users in AWS to represent people who can access your AWS accounts.

As a best practice, it’s strongly recommended that all users managed via AWS SSO set up MFA for their user accounts.

AWS SSO includes the ability to manage permission sets that define which groups of users can access which AWS accounts and the fine grained AWS Identity and Access Management (IAM) permissions associated with this access.  AWS SSO automatically propagates these permissions to each member AWS account in your AWS organization.

## Shared AWS Accounts

Once you’ve signed up for a new AWS account, the “master” account, your cloud administrators will use AWS Control Tower via the Master AWS account to establish a “landing zone” of conventional shared AWS accounts and resources to help provide an initial foundation for your use of AWS. 

Your Master AWS account will be the place in which your cloud administrators will use AWS Control Tower’s [Account Factory](https://docs.aws.amazon.com/controltower/latest/userguide/account-factory.html) via AWS Service Catalog to create new team development accounts, AWS SSO to create and manage groups and users in the locally managed directory, and generally monitor the overall use and health of your AWS environment.

You can grant access to members of your Security and Compliance teams access to the Audit AWS account so that they can easily get into any of the other AWS accounts to review usage and investigate issues.

AWS Control Tower sets up a Log Archive AWS account to secure store AWS platform-wide logs such as AWS CloudTrail logs that record access to all AWS APIs across your AWS accounts and AWS Config logs that record all changes to AWS resources across your AWS accounts.

## Standard AWS Control Tower Guardrails

By using AWS Control Tower, your organization automatically benefits from the set of [built-in guardrails](https://docs.aws.amazon.com/controltower/latest/userguide/guardrails.html) that represent common preventative and detective security controls. AWS Control Tower includes mandatory, strongly recommended, and elective guardrails.

## Next Steps

[Map People to Foundation Functional Roles](1-3-map-people-to-foundation-roles.md)
