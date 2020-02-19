# 5. Determine Initial Networking Approach

In this step your Cloud Administrators will review the initial network design and recommended provisioning methods in support of the development team AWS accounts.

This step should take about 20 minutes to complete.

1. [Review Initial Network Design](#1-review-initial-network-design)
2. [Decide on Initial Provisioning Approach](#2-decide-on-initial-provisioning-approach)
3. [Using Option 1: Customize Account Factory Network Configuration](#3-using-option-1-customize-account-factory-network-configuration)
4. [Using Option 2: Disable Account Factory VPC Provisioning](#4-using-option-2-disable-account-factory-vpc-provisioning)
 

## 1. Review Initial Network Design

As mentioned in the [Initial Development Environment Solution Overview](1-2-solution.md#vpc-network-for-each-development-team-aws-account), it's recommended that you start with a dedicated VPC for each development team AWS account. 

In each VPC you will have a set of public and private subnets. In those AWS regions in which at least 3 Availability Zones (AZs) are availabkle for customer use, it's recommended that your initial set of VPCs have subnets in each of 3 AZs so that your development teams can experiment and perform early testing of workloads that can take advantage of 3 AZs.

At least one public subnet will have a NAT Gateway that enables workloads in any of the private subnets to send traffic outbound to the Internet.

---
**Note: The initial networks will be replaced later on**

Later in your journey, if you set up network connectivity with your on-premises network, you will replace the initial VPCs with configurations that more closely align with your longer term needs. For example, common capabilites that would entail replacing or significantly changing the initial VPCs include:

* **Use of Non Overlapping IP Address Ranges:** So as to avoid complicated network address translation (NAT) configurations, you will likely allocate IP address ranges or "CIDR blocks" to your VPCs that don't overlap with on-premises networks and your other cloud networks.

* **Removal of Public Subnets:** So that your hosting networks have only private subnets and all Internet ingress and egress traffic is routed through centrally managed proxies and security services.

* **Migration to Using a Shared VPC for Development AWS Accounts:** A common solution for multiple development AWS accounts is to provision a single VPC in a network AWS account and share the VPC's subnets with development AWS accounts.  This approach helps consolidate management of VPC resources.

---

---
**Review Note: Why not start with a shared development VPC?**

Given the [benefits](../2-fast-follow-on/2-10-shared-dev-vpc.md) and relative ease of setting it up even at this early stage. i.e create Network AWS accoumt, provision VPC using CloudFormation per this design, ideally with non-overlapping CIDR, and share VPC subnets to the development OU AWS accounts. A 20-minute task.

Later, hooking in on-premises network integration via a site-to-site VPN + Transit Gateway as a fast follow-on is straightforward and doesn't require rework of the dev VPC.

---

![alt text](https://github.com/ckamps/aws-foundation-journey/raw/master/images/dev-network-initial-details.png "Initial Network Details")

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
|2. AWS CloudFormation Template|* Aligned with Infrastructure as Code (Iac).<br><br>* Provides more flexible configuration options that you can easily extend as you progress on your journey.<br><br>* Does not require accessing the master AWS account to manage StackSets.<br><br>* Direct control over naming of cloud resource names that can be helpful in inhibiting write access to foundation resources.<br><br>* Likely aligned with your direction moving forward.|* May require a few minutes of your time to learn how to create stacks from AWS CloudFormation templates.|

---
**Note: AWS Management Console VPC Wizard**

This is another option, but it's a bit more awkward to use as compared to the two options noted above.

* It requires a separate step to obtain an Elastic IP Address.
* It provisions only one private and one public subnet. More subnets can be manually added later.

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

[6. Create Initial Team Development Environments](2-6-create-team-dev-environments.md)