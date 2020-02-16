# 6. Create the Initial Team Development Environments

In this step your Cloud Administrators will create several new team development AWS accounts via AWS Control Tower's Account Factory.

This step should take about 30 minutes to complete.

1. [Use at Least Two Development AWS Accounts from the Start](#1-use-at-least-two-development-aws-accounts-from-the-start)
2. [Create the Development Organizational Unit](#2-create-the-development-organizational-unit)
3. [Create Development Team AWS Accounts](#3-create-development-team-aws-accounts)
4. [Initialize AWS Account System Users](#4-initialize-aws-account-system-users)
5. [Review or Provision Networking](#5-review-or-provision-networking)

## 1. Use at Least Two Development AWS Accounts from the Start

As highlighted previously, an AWS best practice is to isolate the work of distinct development teams by assigning a different AWS account for each team. Benefits of this approach include:

* **Inherent Per Team Cost Allocation:** Since AWS resource costs are, by default, attributable to each AWS account in which the resources are provisioned, at this early stage in your adoption, you don't need to force development teams to use cost allocation tags on their resources.

* **Inherent Isolation Between Teams:** Since cloud resources managed by development teams using different AWS accounts are, by default, completely isolated from each other, complicated AWS Identity and Access Management (IAM) configurations are not needed to ensure that development teams don't inadvertently impact each other's cloud resources.

Initially, you will likely need at least two AWS accounts for the following teams:

|Dev Team Account|Purpose|
|----------------|-------|
|**Application Development Team AWS Account**|A development AWS account for the initial application or data services development team.|
|**Foundation Team AWS Account**|A development AWS account for the initial few Cloud and Security Administrators to experiment, develop, and perform early testing of changes to the foundation.|

## 2. Create the Development Organizational Unit

Moving forward, your company will likely want to apply particular policies or guardrails to all AWS development accounts within your enterprise.  To enable you to easily target such policies across all development AWS accounts, it's recommended that you create a new Organizational Unit (OU) to represent development AWS accounts.

1. As a cloud administrator, use your personal user to log into AWS SSO.
2. Select the AWS master account.
3. Select `Management console` associated with the `AWSAdministratorAccess` role.
4. Select the appropriate AWS region.
5. Navigate to AWS Control Tower.
6. Within the AWS Control Tower dashboard select `Add organizational units`.  
7. Follow the prompts to create a new OU named `development`.

In the next step when you create the new development AWS accounts, you'll specify this new OU.

---
**Note: Your OU design will evolve** 

Since you have the ability to move AWS accounts between OUs and modify OUs, you don't need to perform a complete OU design at this early stage. As you progress on your journey, you will evolve your OU design to suit your emerging needs.  If you'd like to learn more about OUs, see [AWS Organizations in Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/organizations.html).

---

## 3. Create Development Team AWS Accounts

In AWS Control Tower, provision the initial set of AWS development team accounts for early experimentation, development, and testing. 

You'll follow these steps twice: Once to create the initial deveopment team's AWS account and again to create the development AWS account for the foundation team.

1. As a cloud administrator, use your personal user to log into AWS SSO.
2. Select the AWS master account.
3. Select `Management console` associated with the `AWSServiceCatalogEndUserAccess` role.
4. Select the appropriate AWS region.
5. Navigate to AWS Service Catalog.
6. Select `Products list`.
7. Select `AWS Control Tower Account Factory`.
8. Select `Launch Product`.
9. Under `Product Version`, specify a `Name`. This will be the name of the provisioned product in AWS Service Catalog and will not be the name of the new AWS account. For example:
  * `member-account-team-a-dev`
  * `member-account-foundation-dev`
10. Select `Next`.
11. In `Parameters`, consider the following recommendations:

|Field|Recommendation|
|-----|---------------|
|`SSOUserEmail`|Consult the [set of AWS account root user email addresses](2-2-create-master-aws-account.md#3-prepare-email-distribution-lists-for-new-aws-accounts) that you established earlier.|
|`AccountEmail`|Use the same value as `SSOUserEmail`.|
|`SSOUserFirstName`|Use a part of your account name. For example, `Team A` or `Foundation` for the foundation team's development AWS account.|
|`SSOUserLastName`|Use the remaining part of the account name. For example, `Development`|
|`ManagedOrganizationalUnit`|Select the OU you created earlier in this section. For example, `development`|
|`AccountName`|`Team A Development` or `Foundation Development`|

12. Select `Next`.
13. On `Tag Options`, select `Next`.
14. On `Notifications`, select `Next`.
15. Review your account settings, and then select `Launch`. Do not create a resource plan, otherwise the account will fail to be provisioned.

Your account is now being provisioned. It can take a few minutes to complete. You can refresh the page to update the displayed status information. Only one account can be provisioned at a time.

----
**Note: You can change AWS account settings later**

Configuration settings of the AWS accounts you provision via Account Factory shouldn’t be considered static.  Nearly every part of an AWS account can be changed and updated at a later date. See [Account Factory](https://docs.aws.amazon.com/controltower/latest/userguide/account-factory.html) for more details.

---

---
**To Do: Address issue where provisoned products are owned by one user by default**

Based on preliminary testing of this step, only the Cloud Admin who provisions an Account Factory product is able to see and manage that product unless the owner chnages ownership to another user or to an IAM role. This may be expected behavior of AWS Service Catalog, but it runs counter our goal of enabling foundation team members with the same intended access to share in the responsibilities of manging common foundation resources.

We need to verify that this is the default behavior and, if it is, enhance this section to ensure that the resource is shared amongst at least the Cloud Platform team members.

---

## 4. Initialize AWS Account System Users

When each new development team AWS account is created, follow these steps to initialize the AWS account's AWS SSO user and root user to align with security best practices.

### Initialize AWS SSO User for the AWS Account
When a new AWS account has been created via the Account Factory, a user for the new AWS account is created in AWS SSO. As a best practice, you should initiatize the associated user's password and enable MFA. 

1. Access the inbox for the email address you associated with the AWS account when using Account Factory.
2. Within the email message "Invitation to join AWS Single Sign-On", select `Accept invitation`.
3. Follow the process to set the initial password for this user.

Follow the instruction in [How to Register a Device for Use with Multi-Factor Authentication](https://docs.aws.amazon.com/singlesignon/latest/userguide/user-device-registration.html).

### Initialize AWS Account's Root User

In addition to a new AWS SSO user being created for the AWS account, the new AWS account has a built-in root user.  

See [Log In as Root User](https://docs.aws.amazon.com/controltower/latest/userguide/best-practices.html#root-login) in the AWS Control Tower documentation for instructions to set the root user’s password.

See [Enable MFA on the AWS Account Root User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_mfa) for instructions to enable MFA.

## 5. Review or Provision Networking

***...if networking has already been set up via Account Factory for the development AWS accounts, provide a very brief overview of the resulting network topology...***

***...if networking has not been set up via Account Factory, highlight their options to use several other approaches at this stage...***

## Next Steps

[7. Onboarding Your Initial Development Teams](2-7-onboard-dev-teams.md)
