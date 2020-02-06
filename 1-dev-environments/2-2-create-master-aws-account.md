# 2. Create a New Master AWS Account

In this step your Cloud Administrators will use the standard AWS new account creation process to create a new “master” AWS account. 

This step should take about 20 minutes.

## Benefits of Using Multiple AWS Accounts

AWS accounts are coarse grained resource containers that help you isolate and secure different collections of cloud resources and data. Use of multiple AWS accounts can make your use of cloud more secure by providing clear ownership and control boundaries and lowering the blast radius of any particular set of cloud resources. 

In support of your initial need for development environments, this guide leads you through the process to create an initial set of foundation and development team-specific AWS accounts.  In the future, you will create a series of test and production AWS accounts to isolate the formal test and production environments from development environments.

Over the course of your cloud adoption journey, you will likely end up with a number of accounts ranging from a dozen or so to hundreds depending on the size of your application and data services portfolio and the granularity by which you choose to isolate the associated cloud resources and data across your organization and across the software development lifecycle (SDLC).

## Starting With a New Master AWS Account

The initial AWS account that you create will be configured as a new “master” AWS account in which billing for AWS services consumed across accounts will be consolidated and your Cloud Administrators will provision new “member” AWS accounts for development teams.

Even if you have an existing AWS account, we strongly recommend that you establish a new AWS account as the basis of your formal cloud foundation and adoption for several reasons:

1. **AWS Control Tower currently requires a new master AWS account.** Later in this guide, you will be using the AWS Control Tower service to establish an initial set of security guardrails and other capabilities as part of your cloud foundation.
2. **Your existing AWS accounts might not be aligned with AWS best practices.**

After you create your new master AWS account, you can make use of a standard process to move any existing AWS accounts into your new master AWS account so that you can easily consolidate billing and day-to-day management of all of your AWS accounts.

## 1. Prepare Email Distribution Lists for New AWS Accounts

Prepare a set of email distribution lists to represent the root user of each of the new AWS accounts that will be created. In this step you'll be referring to only the email distribution list for the master AWS account. In later steps, when you create other AWS accounts, you'll be entering the email distribution lists for those other AWS accounts.

The following table includes the minimum set of distribution lists to get started. Each AWS account must have a globally unique email address. 

If your organization already has a naming standard for mail addresses associated with services, you should use that standard format and include references to at least "aws" and and an abbreviation of the unique role or purpose of each account.

|AWS Account	|Example Root User Email Distribution List|Example with "+" Style Email Address|
|---|---|---|
|Master|aws-account-master@acme.com|aws-account+master@acme.com|
|Audit|aws-account-audit@acme.com|aws-account+audit@acme.com|
|Log Archive|aws-account-log-archive@acme.com|aws-account+log-archive@acme.com|
|Cloud Platform Team Development|aws-account-cloud-platform-dev@acme.com	|aws-account+cloud-platform-dev@acme.com|
|Team 1 Development|aws-account-team-a-dev@acme.com|aws-account+team-a-dev@acme.com|

**Use of “+” Style Email Addresses**
If your organization’s email system supports the use of “+” style email addresses in which email multiple email addresses are aliased to the same email account, then you might find it beneficial to use this form to consolidate the root user email addresses for either all or collections of AWS accounts to either one or a few actual email accounts.

For example: [aws-account1+master@acme.com](mailto:aws-account1+master@acme.com) and [aws-account1+audit@acme.com](mailto:aws-account1+audit@acme.com) will be treated as unique addresses in AWS but your mail system may deliver the mail to the same [aws-account1@acme.com](mailto:aws-account1@acme.com) email address.

**Role of the AWS Account Root User Email Addresses**
...To Do - state the role of the email addresses... i.e. are notifications sent to them? root access is covered int he next section...

**Controlling Access to Root User Email Accounts**
Since the email address associated with an AWS account is used as the [root user login for the account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html), anyone with access to that email account will have access to password reset process for the account.  

## 2. Create a New AWS Master Account

Visit https://aws.amazon.com/ and click “Create AWS Account” and enter the the required information on the following page.  For this account, use the master account email address you already established. 

**Provide Account Root User’s Email Address**
Since the email address is used to initially access your AWS account, be very careful that you enter the correct email address and that you have access to that email account.

Note: Since AWS Control Tower will be used to establish part of your foundation in a later step and AWS Control Tower currently has limitations on how email addresses for AWS accounts can be changed, you will need to contact AWS Support to change an account’s email address.

**Set Personal or Professional**
Set your account to either personal or professional.  Both types of accounts have the same functionality and features.  Enter your personal or professional information and then read and accept the [AWS Customer Agreement](https://aws.amazon.com/agreement/).

**Provide Billing Information**
At this point, you’ll have an account created and you’ll get a confirmation email.  However, you’ll need to enter billing information before you can continue.

Add a payment method and contact information for the billing method.  You’ll go through a brief account verification process via a mobile device so enter a phone number you have current access to.

*Future consideration:* _Switch your account to invoicing instead of credit card based billing_

**Select a Support Plan**
On the Select a Support Plan page, choose one of the available support plans.  Sine your organization is going to be using AWS for formal development and eventually production purposes, we recommend that you select “Developer” support.  Before you transition any applications or data services to production, we strongly recommend upgrading to Business support.  Once you are preparing to host business critical workloads and data in the cloud, you should consider upgrading to Enterprise support. 

See [AWS Support Plans](https://aws.amazon.com/premiumsupport/plans/) for a description of features and benefits of each level of support.

In a few minutes your account should be fully activated and you’ll receive a confirmation email.  If you don’t, review the troubleshooting steps from the [Create and Activate an AWS Account support page](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)

## 3. Secure Your AWS Account Root User

It’s strongly recommended and an AWS security best practice to enable multi-factor authentication (MFA) to the AWS account root user and to avoid using the root user, even for administrative tasks, from this point forward.

See [Enable MFA on the AWS Account Root User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_mfa) for instructions.

## 4. Create an IAM user for Administrative Bootstrap Purposes

Although you will be provisioning cloud administrator and developer user accounts via the AWS Single Sign-on (SSO) service later in this guide, it is required that you first create an administrative bootstrap user account via the AWS Identity and Access Management (IAM) service and switch to that user to set up the next parts of your initial foundation.

This administrative user should be only used to complete your initial foundation setup and act as a “break glass” user in case access via AWS SSO user accounts encounters an issue.

**Recommendations for Administrative Bootstrap User**

* Since this account will only be used for break glass purposes after your foundation has been established, you don’t need to associate the user with a human user. Instead, you can use a name such as “Administrator”.
* Enable “AWS Management Console access” only for this user. “Programmatic access” should not be necessary for this user.

**Create the Administrative Bootstrap User**
While logged in as the root user, follow the instructions in [Create an IAM user](https://docs.aws.amazon.com/controltower/latest/userguide/setting-up.html#setting-up-iam) to create this administrative user.

Once the user has been created, sign into the AWS Management Console as the user and enable MFA to help secure the account. See [Enable a Virtual MFA Device fo an IAM User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html#enable-virt-mfa-for-iam-user).

## 5. Set Alternate Contacts

Once you’ve set up your bootstrap administrative IAM user, log in as that user and set the Alternate Contacts for your account so that notifications of billing, operations, and security events are routed to the proper teams.  As a best practice, you can use email distribution lists so that notifications are set to multiple people in the same team.

Access [Account  Settings](https://console.aws.amazon.com/billing/home?#/account) in the AWS Management Console to set the Alternate Contacts.

## Next Steps

Proceed to [3. Setting Up an Initial Landing Zone Using AWS Control Tower](2-3-set-up-landing-zone.md)
