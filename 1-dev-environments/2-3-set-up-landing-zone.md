# 3. Set Up an Initial Landing Zone via AWS Control Tower

In this step your Cloud Administrators will use the AWS Control Tower service in your new AWS master account to establish an initial “landing zone” or a foundation of security guardrails and other resources that will help your organization manage use of the AWS platform. You can learn more by reviewing [AWS Control Tower Features](https://aws.amazon.com/controltower/features/).

This step should take about 90 minutes to complete.

To Do: Include a table of contents so that an overview of steps is shown up front...

## 1. Identify Your Preferred AWS Region

Since AWS Control Tower will establish a set of management resources in a “home” AWS region, you need to identify which AWS region you expect to host most of your AWS management resources. You will select this region in the next step.

## 2. Log In as Administrator IAM User

Log in as the Administrator IAM user that you created in the last section before you use AWS Control Tower to set up your initial landing zone.

## 3. Create Landing Zone Using AWS Control Tower

Before using AWS Control Tower to create an initial landing zone, ensure that you review these considerations:

* **Desired Home AWS Region** - Ensure that you select the proper AWS region in the upper right hand side of the AWS Management Console before creating the landing zone. The AWS region you select should be the AWS region in which you expect do perform the majority of your work with AWS and from which you will maintain your foundation.
* **Email Distribution Lists** - Consult the [set of AWS account root user email addresses](2-2-create-master-aws-account.md#1-prepare-email-distribution-lists-for-new-aws-accounts) that you established earlier.
* **Pre-Launch Checks** - Since you’ve just created a new master AWS account, the pre-launch check considerations for creating your landing zone should already be met.

Follow the steps in [Getting Started with AWS Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/getting-started-with-control-tower.html) to set up your landing zone. 

The set up process can take 20-60 minutes to complete.

## 4. Set AWS Account Root User Password and Enable MFA

Since AWS Control Tower creates two new member accounts while setting up the initial landing zone, you should follow AWS security best practices by setting the password and enabling MFA for the root user of each of the following accounts:

* Audit
* Log archive

See [Log In as Root User](https://docs.aws.amazon.com/controltower/latest/userguide/best-practices.html#root-login) in the AWS Control Tower documentation for instructions to set the root user’s password.

See [Enable MFA on the AWS Account Root User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_mfa) for instructions to enable MFA.

## 5. Enable MFA via AWS SSO for the Admin User Created via Control Tower

As part of the landing zone set up, AWS Control Tower creates a Control Tower Administrator user in the AWS Single-Sign On ( AWS SSO) service in your master account.  As a best practice, you should enable MFA for this user.

### Accept Invitation for this User

The email address associated with the AWS master account’s root user will receive an email message containing an invite to activate this user account.  Review the invitation and accept it.

<img src="../images/accept-aws-sso-invitation.png" alt="Accept SSO Invitation" width="400"/>

The email message you recieved also contains a User portal URL that you should bookmar given that it represents the URL to use SSO to access your new AWS environment., we will use it to access the AWS environment throughout the labs.

### Set Password and Activate MFA for the User

On selecting Accept Invitation, you will be redirected to the AWS Single Sign-On page and from where you could set New Password to your master account. Repeat Password and Update User to proceed.

Follow the instruction in [How to Register a Device for Use with Multi-Factor Authentication](https://docs.aws.amazon.com/singlesignon/latest/userguide/user-device-registration.html).

### Receive and Process AWS Organizations Email Message

You will receive one more email with subject AWS Organizations email verification request to the master account email address. Click on Verify your email address to continue with inviting newly created accounts into AWS Organization.

### Receive and Process AWS Notification Email Messages for Each Region

The email address you provided for the audit account will receive AWS Notification - Subscription Confirmation emails from every AWS Region supported by AWS Control Tower. To receive compliance emails in your audit account, you must choose the Confirm subscription link within each email from each AWS Region supported by AWS Control Tower.

## 6. Review AWS Control Tower Best Practices for Administrators

Now that you've set up your initial landing zone, take a few minutes to review [Best Practices for Account Administrators](https://docs.aws.amazon.com/controltower/latest/userguide/best-practices.html#tips-for-admin-maint) so that you understand temporary limitations and other considerations when working with AWS Control Tower.

For example:

* **Managing Organizational Units (OUs)** - AWS Control Tower currently supports only a single level of AWS Organizations Organizational Units (OUs) and creation of OUs to be used with AWS accounts managed by AWS Control Tower must be performed via AWS Control Tower and not via AWS Organizations.
* **Modification of AWS Account Root User Email Addresses** - AWS Control Tower does not currently support self-service modification of the email addresses associated with the root user of each AWS account.  You currently need to contact AWS Support to have these email addresses changed.

## 7. Determine Initial Approach to Virtual Private Cloud (VPC) Configuration

As part of the landing zone established by AWS Control Tower, an “AWS Control Tower Account Factory” product is deployed to AWS Service Catalog in your master account. In a later step in this guide, your Cloud Administrators will use this product to easily create a new AWS member account for each development team. The Account Factory has the ability to provision a basic AWS Virtual Private Cloud (VPC) when it creates a new AWS account.

 At this stage, your Cloud Administrators should make a decision as to whether:

1. An initial set of AWS Virtual Private Cloud (VPC) networks will be created via the Account Factory when each development account is created or 
2. Your Cloud Administrators will create a VPC after each account is created.

 If in this early stage of your cloud adoption you simply need to get basic VPCs deployed with each development account and you aren’t yet ready to connect those networks to on-premises networks and/or to other AWS VPCs, then you can take advantage of the built-in VPC creation of Account Factory and replace these initial VPCs that are compatible with these future requirements at a later time.

 As your networking requirements evolve, you will likely end up replacing the initial VPC you provision for each development account with VPCs that are built using infrastructure as code tools such as AWS CloudFormation and Hashicorp’s Terraform. 

 Key considerations when using the VPC creation feature of Account Factory:

* One set of VPC specifications will be used for all accounts. This means that your initial set of VPCs will have overlapping IP address (CIDR) ranges that make inter-VPC and VPC to on-premises network connectivity difficult.
* Limited flexibility in terms of the VPC subnet topology including the number and role of subnets.

**Not Using Account Factory to Create VPCs**
 If you want more direct control of your VPCs, you can configure the Account Factory to exclude creation of a VPC when creating a new AWS account. See [Configuring AWS Control Tower Without a VPC](https://docs.aws.amazon.com/controltower/latest/userguide/configure-without-vpc.html) for details on disabling automatic creation of VPCs.

 To do: Provide pointer to example CloudFormation template and docs.

**Using Account Factory to Create Initial Temporary VPCs**
 If you choose to use the Account Factory’s built-in support for creating basic VPCs, see the section “Configuring Account Factory with Amazon Virtual Private Cloud Settings” in the [AWS Control Tower Account Factory](https://docs.aws.amazon.com/controltower/latest/userguide/account-factory.html) documentation for setting up the parameters for your initial set of VPCs. 

 To review and modify the VPC settings used by the Account Factory, in the AWS Management Console access AWS Control Tower → Account factory.

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
 
 ## Next Steps
 
[4. Set Up Initial AWS Platform Access Controls](2-4-set-up-aws-platform-access-controls.md)
