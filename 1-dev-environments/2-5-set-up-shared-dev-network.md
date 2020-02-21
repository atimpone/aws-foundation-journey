# 5. Set Up Shared Development Network

In this step your Cloud Administrators will review the initial network design, create a new Network AWS account, provision a shared development network, and share that network will all development AWS accounts in your AWS organization.

This step should take about 60 minutes to complete.

1. [Review Initial Network Design](#1-review-initial-network-design)
2. [Create Organizational Units](#2-create-organizational-units)
3. [Disable Account Factory VPC Provisioning](#3-disable-account-factory-vpc-provisioning)
4. [Create Network AWS Account](#4-create-network-aws-account)
5. [Enable Foundation Team Members Access](#5-enable-foundation-team-members-access)
6. [Determine IP Address CIDR Blocks](#6-determine-ip-address-cidr-blocks)
7. [Provision Development VPC](#7-provision-development-vpc)
8. [Review Development VPC](#8-review-development-vpc)
9. [Share Development VPC with Development OU](#9-share-development-VPC-with-development-ou)

## 1. Review Initial Network Design

As mentioned in the [Initial Development Environment Solution Overview](1-2-solution.md#vpc-network-for-each-development-team-aws-account), it's recommended that you start with a single development VPC that you will share across all development team AWS accounts. 

The shared development VPC will have a set of public and private subnets. In those AWS regions in which at least 3 Availability Zones (AZs) are availabkle for customer use, it's recommended that your initial set of VPCs have subnets in each of 3 AZs so that your development teams can experiment with and perform early testing of workloads and AWS services that can take advantage of 3 AZs.

At least one public subnet will have a NAT Gateway that enables workloads in any of the private subnets to send traffic outbound to the Internet. For example, to enable workloads to download content from Internet accessible source code and package repositories.

As you progress in your journey, you may transition from this initial approach of providing development teams with direct Internet access via the initial set of public subnets and NAT Gateway to a more secure architecture where all Internet egress and ingress traffic is routed through your standard enterprise edge security services. In this future state, development teams would not have access direct to public subnets. This capability is highlighted in the optional [fast follow-on capabilities](../README.md#2-establish-fast-follow-on-capabilities).

![alt text](https://github.com/ckamps/aws-foundation-journey/raw/master/images/dev-network-initial-details.png "Initial Network Details")

## 2. Create Organizational Units

Using AWS Control Tower, create several Organizational Units (OUs) that will act as a mechanism to group AWS accounts that have similar security and management needs.  Initially, the OU structure will simply consist of two custom OUs:

* **`infrastructure`** - For foundation infrastructure related AWS accounts including the Network AWS account that you will create later in this section.
* **`development`** - For development team AWS accounts that you'll create in the next section.

---
**Note: Your OU design will evolve** 

Since you have the ability to move AWS accounts between OUs and modify OUs, you don't need to perform a complete OU design at this early stage. As you progress on your journey, you will evolve your OU design to suit your emerging needs.  If you'd like to learn more about OUs, see [AWS Organizations in Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/organizations.html).

---
### Create the `infrastructure` OU

1. As a Cloud Administrator, use your personal user to log into AWS SSO.
2. Select the AWS **master** account.
3. Select `Management console` associated with the **`AWSAdministratorAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to **`AWS Control Tower`**.
6. Within the AWS Control Tower dashboard select `Add organizational units`.  
7. Follow the prompts to create a new OU named **`infrastructure`**.

In the a subsequent step when you create the new Network AWS account, you'll specify this new OU.

### Create the `development` OU

1. Within the AWS Control Tower dashboard select `Add organizational units`.  
2. Follow the prompts to create a new OU named **`development`**.

In the next section when you create the new development AWS accounts, you'll specify this new OU.

## 3. Disable Account Factory VPC Provisioning

Since you will be provisioning the shared development VPC directly using AWS CloudFormation, you need to ensure that the AWS Control Tower Account Factory network configuration is set to disable creation of a VPC when creating a new AWS account.  Otherwise, the Account Factory will attempt to create a VPC each time you provision a new AWS account.

See [Configuring AWS Control Tower Without a VPC](https://docs.aws.amazon.com/controltower/latest/userguide/configure-without-vpc.html) for details on disabling automatic creation of VPCs.

## 4. Create Network AWS Account

In AWS Control Tower, provision the Network AWS account that will initially contain the shared development VPC. Later in your joruney, you'll deploy more network related resources to this AWS account. 

---
**Note:** Use the `AWSServiceCatalogEndUserAccess` role**

In the following steps, it's important that you select the correct role when accessing the master AWS account. Failure to do so, will result in you not being able to work with AWS Service Catalog to provision the new AWS account.

---

1. As a Cloud Administrator, use your personal user to log into AWS SSO.
2. Select the AWS **master** account.
3. Select `Management console` associated with the **`AWSServiceCatalogEndUserAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to **`AWS Service Catalog`**.
6. Select `Products list`.
7. Select `AWS Control Tower Account Factory`.
8. Select `Launch Product`.
9. Under `Product Version`, specify a `Name`. For example, **`member-account-network`**.
10. Select `Next`.
11. In `Parameters`, consider the following recommendations:

|Field|Recommendation|
|-----|---------------|
|`SSOUserEmail`|Consult the [set of AWS account root user email addresses](1-4-address-pre-requisites.md#1-create-email-distribution-lists-for-new-aws-accounts) that you established earlier.|
|`AccountEmail`|Use the same value as `SSOUserEmail`.|
|`SSOUserFirstName`|Use a part of your account name. For example, `Network`.|
|`SSOUserLastName`|Use the remaining part of the account name. For example, `Infrastructure`|
|`ManagedOrganizationalUnit`|Select the infrastructure OU you created earlier in this section. For example, **`infrastructure`**.|
|`AccountName`|**`Network`**|

12. Select `Next`.
13. On `Tag Options`, select `Next`.
14. On `Notifications`, select `Next`.
15. Review the account settings, and then select `Launch`. Do not create a resource plan, otherwise the account will fail to be provisioned.

The AWS account is now being provisioned. It can take a few minutes to complete. You can refresh the page to update the displayed status information.

----
**Note: You can change AWS account settings later**

Configuration settings of the AWS accounts you provision via Account Factory shouldn’t be considered static.  Nearly every part of an AWS account can be changed and updated at a later date. See [Account Factory](https://docs.aws.amazon.com/controltower/latest/userguide/account-factory.html) for more details.

---

---
**Review Note: Address issue where provisoned products are owned by one user by default**

Based on preliminary testing of this step, only the Cloud Admin who provisions an Account Factory product is able to see and manage that product unless the owner chnages ownership to another user or to an IAM role. This may be the expected behavior of AWS Service Catalog, but it runs counter to our goal of enabling foundation team members who are playing the same functional role to share in the responsibilities of manging common foundation resources.

We need to verify that this is the default behavior and, if it is, enhance this section to ensure that the resource is shared amongst at least the Cloud Administration team members.

---

## 5. Enable Foundation Team Members Access

Since Cloud Administrators won't automatically be granted sufficient access to newly created AWS account, you need to enable this access each time you create a new AWS account via AWS Control Tower's Account Factory.

1. As a Cloud Administrator, use your personal user to log into AWS SSO.
2. Select the AWS **master** account.
3. Select `Management console` associated with the **`AWSAdministratorAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to **`AWS SSO`**.
6. Access `AWS accounts` in AWS SSO.
7. Select the checkbox next to the **`Network`** AWS account.
8. Select `Assign users`.
9. Select `Groups`.
10. Select the checkbox next to the group **`acme-cloud-admin`** or similar.
11. Select `Next: Permission sets`.
12. Select the checkbox next to `AWSAdministratorAccess`.
13. Select `Finish`.

Now you've enabled all users who are part of the Cloud Administrator group in AWS SSO administrator access to the Network AWS account.

## 6. Determine IP Address CIDR Blocks

If you're just experimenting and don't care which CIDR block is used to build the VPC, you can move to the next step, [7. Provision Development VPC](#7-provision-development-vpc).

Otherwise, if you have a formally assigned CIDR block to use, in this step you'll:

1. Review Default VPC Topology
2. Determine VPC CIDR Block
3. Determine Subnet CIDR Blocks

### Review Default VPC Topology

The default parameters of the CloudFormation template will result in a VPC with:
* 2 tiers of subnets: 
  * Public tier
  * Private tier
* 3 subnets for each tier.
* Subnets are mapped across 3 Availability Zone (AZ).

To keep things simple, you can size the subnets identically.

The AWS CloudFormation template that you'll use in the next step to provision the VPC supports the following CIDR block related parameters.

|CIDR Block    |CloudFormation Parameter Name|Purpose|
|--------------|-----------------------------|-------|
|VPC|`pCidr`|The overall CIDR block for the VPC. Although you cannot change this assignment later, you can add another CIDR block to augment the original block.|
|**Public Subnets**||
|Public Subnet 1|`pTier1Subnet1Cidr`|A subset of the VPC CIDR block.|
|Public Subnet 2|`pTier1Subnet2Cidr`|A subset of the VPC CIDR block.|
|Public Subnet 3|`pTier1Subnet3Cidr`|A subset of the VPC CIDR block.|
|**Private Subnets**||
|Private Subnet 1|`pTier2Subnet1Cidr`|A subset of the VPC CIDR block.|
|Private Subnet 2|`pTier2Subnet2Cidr`|A subset of the VPC CIDR block.|
|Private Subnet 3|`pTier2Subnet3Cidr`|A subset of the VPC CIDR block.|

### Determine VPC CIDR Block

If your Network team has supplied a relatively large non-overlapping CIDR block, for example a `/16` - `/20`, you should consider using only a subset of that block for your shared development VPC.  Otherwise, if you've been allocated a `/20` - `/22`, then you should use the entire block for the VPC.

If you need to break down a larger block:

1. Acess the [Visual Subnet Calculator](http://www.davidc.net/sites/default/subnets/subnets.html). 
2. Enter your network address without the mask portion `/nn` the `Network Address` field.
3. Enter the size of allocated block in the `Mask bits` field.
4. Click `Update`.  
5. In the table at the bottom, click the `Divide` link to break down the block into smaller blocks.  

When you've reached block sizes from `/20` - `/22`, select a block size of most interest to you and record that CIDR range so that you can use it in the next step.

### Determine Subnet CIDR Blocks

Once you've determined the VPC CIDR block, breaking it down into an equal size block per subnets is straightforward. 

1. Access the [Visual Subnet Calculator](http://www.davidc.net/sites/default/subnets/subnets.html)
2. Enter your network address without the mask portion `/nn` the `Network Address` field.
3. Enter the size of allocated block in the `Mask bits` field.
4. Click `Update`.  
5. In the table at the bottom, click the `Divide` links to start subdividing the larger block into 6 blocks of equal size.
6. Note the first 6 blocks and supply them as the subnet CIDR blocks in the next step.

## 7. Provision Development VPC

You can use this [sample AWS CloudFormation template](https://github.com/ckamps/infra-aws-vpc-multi-tier) to easily deploy your shared development network.

Download the sample AWS CloudFormation template [infra-multi-tier-vpc.yml](https://raw.githubusercontent.com/ckamps/infra-aws-vpc-multi-tier/master/infra-vpc-multi-tier.yml) to your desktop.

---
**Review Note:  Better VPC CloudFormation example?**

If you're aware of a better CloudFormation template example that is maintained in the `aws-samples` or similar AWS-managed GitHub organizations, provide that feedback. In the meantime, we've started the process to get this example introduced into the `aws-samples` organization.

---

Next, access the new Network AWS account:

1. As a Cloud Administrator, use your personal user to log into AWS SSO.
2. Select the **Network** AWS account.
3. Select `Management console` associated with the **`AWSAdministratorAccess`** role.
4. Select the appropriate AWS region.

Now create a new AWS CloudFormation stack using the sample template you downloaded to your desktop:

1. Navigate to **`CloudFormation`**.
2. Select `Create stack` and `With new resources`.
3. Select `Upload a template file`.
4. Select `Choose file` to select the downloaded template file from your desktop.
5. Select `Next`.
6. Enter a `Stack name`. For example, `dev-vpc`.
7. In `Parameters`:

|Parameter|Guidance|
|---------|--------|
|**`Business Scope`**|Replace `acme` with your organization identifier or stock ticker if that applies. This value is used as a prefix in the name of some of the VPC-related cloud resources.|
|**`VPC Name`**|Change to **`dev`**.|
|**`*Cidr`**|**Just Experimenting**<br><br>If you want to just experiment at this point and don't care about using formally assigned IP address ranges, you can leave the CIDR block parameters at their default values.<br><br>**You Have Your Own CIDR Blocks**<br><br>Enter values for the `pVpcCidr`, `pTier1..`, and `pTier2...` CIDR blocks from the prior step. You can ignore the `pTier3...` parameters because only two tiers - public and private - are being provisioned by default.|

Leave all of the other parameters at their default settings unless you're comfortable changing them.  You can always easily create another stack to experiment with other parameter values. Review the [README](https://github.com/ckamps/infra-aws-vpc-multi-tier) for details on parameters.

7. Select `Next`.
8. Select `Next`.
9. Scrolls to the bottom and mark the checkbox to acknowledge that IAM resources will be created.
10. Select `Create stack`.

In the `Events` tab, monitor the progress of the stack creation process. After 5 or so minutes, creation of the stack should complete.

## 8. Review Development VPC

Review the newly created VPC and associated resources.

1. Navigate to **`VPC`**.
2. Select the VPC and review its details.
3. Select `Subnets` in the left menu and review. By default, you will see 6 subnets.
4. Select `Route Tables` and review. You will see one route table per subnet in addition to the VPC's main route table.
5. Select `NAT Gateways` and review. With the default behavior of the CloudFormation template, a single NAT Gateway will be created.
6. Select `Elastic IPs` and review.  You will see one EIP allocated for each NAT Gateway.
7. Navigate to **`CloudWatch`**.
8. Select `Log groups`.
9. Select the log group associated with the VPC Flow Logs. For example, `/infra/shared/flowlogs`.
10. Explore the log streams. You should see a log stream for each Elastic Network Interface (ENI) used in the VPC. For example, each NAT Gateway has one ENI. Each entry in a log stream represents a the source, destination, and other overall information about the network traffic flowing through the ENI.

## 9. Share Development VPC With Development OU

Now that the development VPC has been provisioned, you need to share the subnets of the VPC with all of the AWS accounts that will become part of the `development` OU that you created earlier.  

### Enable Resource Sharing in AWS Organizations

This is a one time operation.

1. As a Cloud Administrator, use your personal user to log into AWS SSO.
2. Select the AWS **master** account.
3. Select `Management console` associated with the **`AWSAdministratorAccess`** role.
4. Navigate to **`Resource Access Manager`**.
5. Select `Settings`.
6. Select **`Enable sharing with AWS Organizations`**.

### Obtain the ID of the `development` OU

While you're in the master AWS account, obtain and record the resource ID of the **`development`** OU.

1. Navigate to **`AWS Control Tower`**.
2. Select `Organizational units`.
3. Select **`development`**.
4. Copy the `ID` of the form `ou-szfb-rixl8jqc` (example) so that you can refer to it in the next step.

### Create a Resource Share

1. As a Cloud Administrator, use your personal user to log into AWS SSO.
2. Select the **Network** AWS account.
3. Select `Management console` associated with the **`AWSAdministratorAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to **`Resource Access Manager`**.
6. Select `Create a resource share`.
7. Enter a `Name` of **`dev-vpc`**.
8. Under `Resources`, by default, the subnets that were just provisioned should be listed.
9. Select the checkbox to select all of the subnets.
10. Under `Principals`, uncheck `Allow external accounts` given that we're sharing the subnets only with other AWS accounts within this AWS organization.
11. In the search field, copy the organization ID of the **`development`** OU. 
12. Select the matched OU.
13. Select `Create resource share`.

---
**Note: Sharing of names of VPC subnets**

If you were to list the shared VPC subnets from within the development AWS accounts, you would notice that the subnet names are blank.  Currently, sharing of subnets does not include automatic propagation of resource tags, including the `Name` tag. 

As a workaround, in a subsequent section where you provision the development AWS accounts, you can manually assign names to the shared subnets so that it will be easier for the development teams to understand the role of each subnet. For example, more readily distinguishing between public and private subnets.

---

 ## Next Steps

[6. Create Initial Team Development Environments](2-6-create-team-dev-environments.md)
