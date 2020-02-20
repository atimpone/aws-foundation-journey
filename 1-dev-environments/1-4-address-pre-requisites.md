# Address Pre-Requisites

In this step the few people who are leading the effort to establish the initial development environment and supporting foundation will address a few technical pre-requsites before the build out of the environment begins.

1. [Create Email Distribution Lists for New AWS Accounts](#1-create-email-distribution-lists-for-new-aws-accounts)
2. [Obtain Non-Overlapping IP Address Range](#2-obtain-non-overlapping-ip-address-range)

## 1. Create Email Distribution Lists for New AWS Accounts

Prepare a set of email distribution lists to represent the root user of each of the new AWS accounts that will be created. In this step you'll be referring to only the email distribution list for the master AWS account. In later steps, when you create other AWS accounts, you'll be referring to the email distribution lists for those other AWS accounts.

The following table includes the minimum set of distribution lists to get started. Each AWS account must have a globally unique email address. 

If your organization already has a naming standard for mail addresses associated with services, you should use that standard format and include references to at least "aws" and and an abbreviation of the unique role or purpose of each account.

|AWS Account	|Example Distribution List|Example with "+" Style Email Address|
|---|---|---|
|**Foundation AWS Accounts**||
|Master|aws-account-master@acme.com|aws-account+master@acme.com|
|Audit|aws-account-audit@acme.com|aws-account+audit@acme.com|
|Log Archive|aws-account-log-archive@acme.com|aws-account+log-archive@acme.com|
|Network|aws-account-network@acme.com|aws-account+network@acme.com|
|**Development Team AWS Accounts**|||
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

In this step you should consult with your Network team to obtain a suitably sized, non-overlapping IP address range or [CIDR block](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) that can be used not only for the initial shared development network that will be set up in this guide, but also to accomodate test and and production networks that you will provision on AWS as you progress in your journey.

Since your organization will likely interconnect at least a portion of your on-premises networks to your emerging AWS hosted networks, a best practice is to assign a large IP address range or CIDR block for use in AWS that does not overlap with your existing allocated IP addresses. By using non-overlapping IP address ranges, your organization will avoid needing to introduce a complicated network address translation (NAT) solution.

### Recommended IP Address Range Size

Ideally, taking into account future networks beyond the initial development network, you should obtain for your organization's use of AWS overall, an IP address range or CIDR block of at least size `/18` to `/16` or 16,382 to 65,534 IP addresses.

If the desired sizes of non-overlapping CIDR block cannot be obtained at this stage, you should obtain a block of at least size `/22` or 1,022 IP addresses to address the initial shared development network.  You can obtain additional non-overlapping CIDR blocks later to support your build out of test and production networks.

---
**Note: Don't be lulled into thinking a particular CIDR block is large enough**

Although 1,000 IP addresses may sound like a lot, don't be fooled into obtaining too small of a CIDR block.  Since your initial shared development environment will likely have at least 4 subnets, when you divide a `/22` CIDR block of 1,022 IP addresses across the 4 subnets, you end up with only 254 IP available addresses per subnet. Using a `/23` would leave only 126 IP addresses per subnet. Depending on the number of workloads your infrastructure and development teams will be experimenting and testing, these numbers can end up being pretty modest.

---

### Unable to Obtain Non-Overlapping IP Address Range

If you cannot obtain a non-overlapping CIDR block at this stage, you can temporarily use an overlapping block for your initial shared development network. 

In the future, when you need to interconnect a portion of your existing on-premises network, you will need to create a new VPC with a non-overlapping CIDR block, migrate the workloads to the new VPC, and decommission the old VPC.

### Resources

* [VPC and Subnet Sizing for IPv4](https://docs.aws.amazon.com/vpc/latest/userguide//VPC_Subnets.html#vpc-sizing-ipv4)

* [Visual Subnet Calculator](http://www.davidc.net/sites/default/subnets/subnets.html)

## Next Steps

[Build Out the Environment](../README.md#build-out-the-environment)
