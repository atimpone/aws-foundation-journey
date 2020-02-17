# 6. Determine Initial Networking Approach

In this step your Cloud Administrators will review the initial network design and recommended provisioning methods in support of the development team AWS accounts.

This step should take about 20 minutes to complete.

1. [Review Initial Network Design](#1-review-initial-network-design)
2. [Decide on Initial Provisioning Approach](#2-decide-on-initial-provisioning-approach)
3. [Using Option 1: Customize Account Factory Network Configuration](#3-using-option-1-customize-account-factory-network-configuration)
4. [Using Option 2: Disable Account Factory VPC Provisioning](#4-using-option-2-disable-account-factory-vpc-provisioning)
 

## 1. Review Initial Network Design

As mentioned in the Initial [Development Environment Solution Overview](1-2-solution.md#vpc-network-for-each-development-team-aws-account), it's recommended that you start with a network design consisting of a dedicated VPC for each development team AWS account including a set of public and private subnets.

![alt text](https://github.com/ckamps/aws-foundation-journey/raw/master/images/dev-network-initial-details.png "Initial Network Details")

---
**Review Note: Network Configuration Options**

* **One or Multple NAT Gateways?:** Given that these networks will be replaced down the line, should we recommend a single NAT Gateway or go with the NAT Gateway per public subnet?  Due to cost considerations, we may want to recommend a single NAT Gateway for this temporary network.

* **Two or Three AZs?:** Do some AWS services require 3 AZs? If so, where 3 are available, should we recommend 3 by default?

---
**Note: The initial networks will likely be replaced later on**

Later in your journey, if and when you set up network connectivity with your on-premises network, you will likely replace these initial VPCs with configurations that more closely align with your longer term needs. For example, common capabilites that would entail replacing or significantly changing the initial VPCs include:

* **Use of Non Overlapping IP Address Ranges:** So as to avoid complicated network address translation (NAT) configurations, you will likely allocate IP address ranges or "CIDR blocks" to your VPCs that don't overlap with on-premises networks.

* **Removal of Public Subnets:** So that your hosting networks have only private subnets and all Internet ingress and egress traffic is routed through centrally managed proxies and security services.

---

## 2. Decide on Initial Provisioning Approach

You have a vareity of options for provioning VPCs in your development AWS accounts, but the following few options are recommended at this early stage in your journey. You'll have the ability to change your provisioning approach and even use different approaches at the same time for different VPCs.
 
### Option 1: AWS Control Tower Account Factory

As part of the landing zone established by AWS Control Tower, an “AWS Control Tower Account Factory” product is deployed to AWS Service Catalog in your master account.  In a later step in this guide, your Cloud Administrators will use this product to create a new AWS member account for each development team. The Account Factory has the ability to provision a basic AWS Virtual Private Cloud (VPC) when it creates a new AWS account. If you choose this option, a step below helps you configure it to meet your needs.

### Option 2: AWS CloudFormation Template

After you create each development team AWS account, you would use AWS CloudFormation either from the AWS Management Console or command line to create a new CloudFormation stack based on a CloudFormation template file that automatically provisions a VPC and related resources. You supply a series of parameters to customize the VPC configuration. Over time, you can easily evolve the template to meet your changing needs.

### Deciding on an Approach

Use the following table to help you decide which approach to take to provision the VPCs for the first few development team AWS accounts.

|Option|Pros|Cons|
|------|----|----|
|1. AWS Control Tower Account Factory|* Ready-to-use as part of Account Factory.<br><br>* Since it uses AWS CloudFormation, you can modify the VPC resources to some extent after the fact.|* In order to use different IP address ranges for each development AWS account, you'll need to keep changing the AWS Control Tower settings.<br><br>* Configuration options can be confusing in terms of number of subnets per type and number of AZs.<br><br>* Given the relative simplicity of the current implementation, this option probably won't be the method you'll use as you progress on your journey.<br><br>* Although it uses AWS CloudFormation to provision the VPC resources, it uses AWS CloudFormation StackSets managed from the master AWS account.|
|2. AWS CloudFormation Template|* Aligned with Infrastructure as Code (Iac).<br><br>* Provides more flexible configuration options that you can easily extend as you progress on your journey.<br><br>* Does not require accessing the master AWS account to manage StackSets.<br><br>* Likely aligned with your direction moving forward.|* May require a few minutes of your time to learn how to create stacks from AWS CloudFormation templates.|

---
**Note: AWS Management Console VPC Wizard**

This is another option, but it's a bit more awkward to use as compared to the two options noted above.

* It requires a separate step to obtain an Elastic IP Address.
* It provisions only one private and one public subnet. More subnets can be manually added later.
* Since it doesn't use AWS CloudFormation, removing the VPC and the associated resources is a bit more work than simply deleting an AWS CloudFormation stack.

---

## 3. Using Option 1: Customize Account Factory Network Configuration

If you choose to use the AWS Control Tower Account Factory’s built-in support for creating basic VPCs, customize the network configuration options:

1. As a cloud administrator, use your personal user to log into AWS SSO.
2. Select the AWS **master** account.
3. Select Management console associated with the **`AWSAdministratorAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to AWS Control Tower.
6. Select `Account factory`.
7. Select `Edit` to edit the Account Factory network configuration.
8. Use the following guidance to update the configuration:

|Setting|Guidance|
|-------|--------|
|Internet-accessible subnet|Assuming that your development teams’ AWS accounts need access to resources on the Internet, you should enable the “Internet-accessible subnet” option.|
|Maximum number of private subnets|To enable your developers to develop and test using multiple AWS Availability Zones (AZs), you should select “2” for the “Maximum number of private subnets”.|
|Address range|If you don’t expect that your initial VPCs will need to have connectivity with your on-premises networks, you can select any valid network. See [VPC and Subnet Sizing for IPv4](https://docs.aws.amazon.com/vpc/latest/userguide//VPC_Subnets.html#vpc-sizing-ipv4) in the Amazon Virtual Private Cloud documentation for recommendations on IP address ranges and sizes.<br><br>Note that the VPC created in each development team AWS account will be assigned the same IP address range. This overlap might be acceptable to you in the early stages of your use of AWS, but will likely become a barrier as your foundation needs expand.
|Regions for VPC creation|Select only the single AWS region in which your organization expects to do most of its initial work. You’ll likely want to choose the same AWS region as you selected for the AWS Control Tower home region.|

## 4. Using Option 2: Disable Account Factory VPC Provisioning

If you plan to use AWS CloudFormation directly, you should ensure that the AWS Control Tower Account Factory network configuration is set to disable creation of a VPC when creating a new AWS account. 

See [Configuring AWS Control Tower Without a VPC](https://docs.aws.amazon.com/controltower/latest/userguide/configure-without-vpc.html) for details on disabling automatic creation of VPCs.

 ## Next Steps

[7. Create Initial Team Development Environments](2-7-create-team-dev-environments.md)
