# 6. Determine Initial Networking Approach

In this step your Cloud Administrators will review options and make decisions for both the initial network design and provisioning methods in support of the development team AWS accounts.

This step should take about 30 minutes to complete.

## 1. Decide on Initial Network Design

As mentioned in the Initial [Development Environment Solution Overview](1-2-solution.md#vpc-network-for-each-development-team-aws-account), it's recommended that you start with a two-tier network design consisting of a dedicated VPC for each development team AWS account including a set of public subnets and a set of private subnets.  

...

### Set Expectations for Replacing These Networks in the Future

Later in your journey, if and when you set up network connectivity with your on-premises network, you will likely replace these initial VPCs with VPCs that more closely align with your longer term needs. For example, in the future, to avoid complicated network address translation (NAT) configurations, you will likely allocate IP address ranges or "CIDR blocks" to your VPCs that don't overlap with on-premises networks.

## 2. Decide on Initial Networking Provisioning Approach

As part of the landing zone established by AWS Control Tower, an “AWS Control Tower Account Factory” product is deployed to AWS Service Catalog in your master account. In a later step in this guide, your Cloud Administrators will use this product to easily create a new AWS member account for each development team. The Account Factory has the ability to provision a basic AWS Virtual Private Cloud (VPC) when it creates a new AWS account.

 At this stage, your Cloud Administrators should make a decision as to whether:

1. An initial set of AWS Virtual Private Cloud (VPC) networks will be created via the Account Factory when each development account is created or 
2. Your Cloud Administrators will create a VPC after each account is created.

 If in this early stage of your cloud adoption you simply need to get basic VPCs deployed with each development account and you aren’t yet ready to connect those networks to on-premises networks and/or to other AWS VPCs, then you can take advantage of the built-in VPC creation of Account Factory and replace these initial VPCs that are compatible with these future requirements at a later time.

 As your networking requirements evolve and you become skilled in Infrastructure as Code (IaC) tools and practices, you will likely end up replacing the initial VPC you provision for each development account with VPCs that are built using IaC tools such as AWS CloudFormation and Hashicorp’s Terraform. 

 Key considerations when using the VPC creation feature of Account Factory:

* One set of VPC specifications will be used for all accounts. This means that your initial set of VPCs will have overlapping IP address (CIDR) ranges that make inter-VPC and VPC to on-premises network connectivity difficult.
* Limited flexibility in terms of the VPC subnet topology including the number and role of subnets.

## 3. Configure Account Factory's VPC Settings

If you choose to use the AWS Control Tower Account Factory’s built-in support for creating basic VPCs, see the section “Configuring Account Factory with Amazon Virtual Private Cloud Settings” in the [AWS Control Tower Account Factory](https://docs.aws.amazon.com/controltower/latest/userguide/account-factory.html) documentation for setting up the parameters for your initial set of VPCs. 

If you've chosen to use another method to provision the initial set of VPCs, skip this step and proceed to [4. Disable Account Factory's VPC Creation](#4-disable-account-factorys-vpc-creation)

 To review and modify the VPC settings used by the Account Factory, in the AWS Management Console access `AWS Control Tower → Account factory`.

<img src="../images/control-tower-account-factory-network-settings.png" alt="AWS Control Tower Account Factory Network Settings" width="400"/>

**Internet-accessible subnet**
 Assuming that your development teams’ AWS accounts need access to resources on the Internet, you would enable the “Internet-accessible subnet” option.

**Maximum number of private subnets**
 To enable your developers to develop and testing using multiple AWS Availability Zones (AZs), you should select “2” for the “Maximum number of private subnets”.

**Address range**
 If you don’t expect that your initial VPCs will need to have connectivity with your on-premises networks, you can select any valid network. See [VPC and Subnet Sizing for IPv4](https://docs.aws.amazon.com/vpc/latest/userguide//VPC_Subnets.html#vpc-sizing-ipv4) in the Amazon Virtual Private Cloud documentation for recommendations on IP address ranges and sizes. 

 Note that the VPC created in each development team AWS account will be assigned the same IP address range. This overlap might be acceptable to you in the early stages of your use of AWS, but will likely become a barrier as your foundation needs expand.

**Regions for VPC creation**
 Select only the single AWS region in which your organization expects to do most of its initial work. You’ll likely want to choose the same AWS region as you selected for the AWS Control Tower home region.

## 4. Disable Account Factory's VPC Creation

 If you want more direct control of your VPCs, you can configure the Account Factory to exclude creation of a VPC when creating a new AWS account. See [Configuring AWS Control Tower Without a VPC](https://docs.aws.amazon.com/controltower/latest/userguide/configure-without-vpc.html) for details on disabling automatic creation of VPCs.

 ## Next Steps

[7. Create Initial Team Development Environments](2-7-create-team-dev-environments.md)
