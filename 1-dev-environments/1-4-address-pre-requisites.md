# Address Pre-Requisites

In this step the few people who are leading the effort to establish the initial development environment and supporting foundation will address a few technical pre-requsites before the build out of the environment begins.

1. [Create Email Distribution Lists for New AWS Accounts](#1-create-email-distribution-lists-for-new-aws-accounts)
2. [Obtain Non-Overlapping IP Address Range](#2-obtain-non-overlappin-ip-address-range)

## 1. Create Email Distribution Lists for New AWS Accounts

Prepare a set of email distribution lists to represent the root user of each of the new AWS accounts that will be created. In this step you'll be referring to only the email distribution list for the master AWS account. In later steps, when you create other AWS accounts, you'll be referring to the email distribution lists for those other AWS accounts.

The following table includes the minimum set of distribution lists to get started. Each AWS account must have a globally unique email address. 

If your organization already has a naming standard for mail addresses associated with services, you should use that standard format and include references to at least "aws" and and an abbreviation of the unique role or purpose of each account.

|AWS Account	|Example Root User Email Distribution List|Example with "+" Style Email Address|
|---|---|---|
|Foundation AWS Accounts||
|Master|aws-account-master@acme.com|aws-account+master@acme.com|
|Audit|aws-account-audit@acme.com|aws-account+audit@acme.com|
|Log Archive|aws-account-log-archive@acme.com|aws-account+log-archive@acme.com|
|Network|aws-account-network@acme.com|aws-account+network@acme.com|
|Development Team AWS Accounts|||
|Foundation Team Development|aws-account-foundation-dev@acme.com|aws-account+foundation-dev@acme.com|
|Team 1 Development|aws-account-team-a-dev@acme.com|aws-account+team-a-dev@acme.com|

### Use of “+” Style Email Addresses
If your organization’s email system supports the use of “+” style email addresses in which email multiple email addresses are aliased to the same email account, then you might find it beneficial to use this form to consolidate the root user email addresses for either all or collections of AWS accounts to either one or a few actual email accounts.

For example: [aws-account1+master@acme.com](mailto:aws-account1+master@acme.com) and [aws-account1+audit@acme.com](mailto:aws-account1+audit@acme.com) will be treated as unique addresses in AWS but your mail system may deliver the mail to the same [aws-account1@acme.com](mailto:aws-account1@acme.com) email address.

---
**Note: Office 365 users**

It appears that plus style addressing is on the [Office 365 roadmap for 2020](https://techcommunity.microsoft.com/t5/exchange-team-blog/exchange-transport-news-from-microsoft-ignite-2019/ba-p/993417).

---

### Controlling Access to Root User Email Accounts
Since the email address associated with an AWS account is used as the [root user login for the account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html), anyone with access to that email account will have access to password reset process for the account.  

## 2. Obtain Non-Overlapping IP Address Range

...

## Next Steps

[1. Create Master AWS Account](2-1-create-master-aws-account.md)