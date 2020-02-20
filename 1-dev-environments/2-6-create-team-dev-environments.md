# 6. Create Initial Team Development Environments

In this step your Cloud Administrators will create several new team development AWS accounts via AWS Control Tower's Account Factory.

This step should take about 30 minutes to complete.

1. [Use at Least Two Development AWS Accounts from the Start](#1-use-at-least-two-development-aws-accounts-from-the-start)
2. [Create Development Team AWS Accounts](#2-create-development-team-aws-accounts)
3. [Initialize AWS Account System Users](#3-initialize-aws-account-system-users)
4. [Provide Cloud Administrators Access to New AWS Accounts](#4-provide-cloud-administrators-access-to-new-aws-accounts)
5. [Apply Names to Shared VPC Resources](#5-apply-names-to-shared-vpc-resources)

## 1. Use at Least Two Development AWS Accounts from the Start

As highlighted previously, an AWS best practice is to isolate the work of distinct development teams by assigning a different AWS account to each team. Benefits of this approach include:

* **Inherent Per Team Cost Allocation:** Since AWS resource costs are, by default, attributable to each AWS account in which the resources are provisioned, at this early stage in your adoption, you don't need to force development teams to use cost allocation tags on their resources.

* **Inherent Isolation Between Teams:** Since cloud resources managed by development teams using different AWS accounts are, by default, completely isolated from each other, complicated AWS Identity and Access Management (IAM) configurations are not needed to ensure that development teams don't inadvertently impact each other's cloud resources.

Initially, you will likely need AWS accounts for the following teams:

|Dev Team Account|Purpose|
|----------------|-------|
|**Application Development Team AWS Account**|A development AWS account for the initial application or data services development team.|
|**Foundation Team AWS Account**|A development AWS account for the initial few Cloud and Security Administrators to experiment, develop, and perform early testing of changes to the foundation.|

## 2. Create Development Team AWS Accounts

In AWS Control Tower, provision the initial set of AWS development team accounts for early experimentation, development, and testing. 

You'll follow these steps twice: Once to create the initial deveopment team's AWS account and again to create the development AWS account for the foundation team.

1. As a Cloud Administrator, use your personal user to log into AWS SSO.
2. Select the AWS **master** account.
3. Select `Management console` associated with the **`AWSServiceCatalogEndUserAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to **`AWS Service Catalog`**.
6. Select `Products list`.
7. Select `AWS Control Tower Account Factory`.
8. Select `Launch Product`.
9. Under `Product Version`, specify a `Name`. This will be the name of the provisioned product in AWS Service Catalog and will not be the name of the new AWS account. For example:
  * **`member-account-team-a-dev`**
  * **`member-account-foundation-dev`**
10. Select `Next`.
11. In `Parameters`, consider the following recommendations:

|Field|Recommendation|
|-----|---------------|
|`SSOUserEmail`|Consult the [set of AWS account root user email addresses](1-4-address-pre-requisites.md#1-create-email-distribution-lists-for-new-aws-accounts) that you established earlier.|
|`AccountEmail`|Use the same value as `SSOUserEmail`.|
|`SSOUserFirstName`|Use a part of your account name. For example, `Team A` or `Foundation` for the foundation team's development AWS account.|
|`SSOUserLastName`|Use the remaining part of the account name. For example, `Development`|
|`ManagedOrganizationalUnit`|Select the development OU you created earlier. For example, **`development`**|
|`AccountName`|`Team A Development` or `Foundation Development`|

12. Select `Next`.
13. On `Tag Options`, select `Next`.
14. On `Notifications`, select `Next`.
15. Review your account settings, and then select `Launch`. Do not create a resource plan, otherwise the account will fail to be provisioned.

The AWS account is now being provisioned. It can take a few minutes to complete. You can refresh the page to update the displayed status information.

## 3. Initialize AWS Account System Users

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

## 4. Provide Cloud Administrators Access to New AWS Accounts

Since Cloud Administrators won't automatically be granted sufficient access to newly created AWS accounts, you need to enable this access each time you create new AWS accounts via AWS Control Tower's Account Factory.

1. As a Cloud Administrator, use your personal user to log into AWS SSO.
2. Select the AWS **master** account.
3. Select `Management console` associated with the **`AWSAdministratorAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to **`AWS SSO`**.
6. Access `AWS accounts` in AWS SSO.
7. Select the checkboxes next both development AWS accounts. For example:
  * `Team A - Dev`
  * `Foundation - Dev`
8. Select `Assign users`.
9. Select `Groups`.
10. Select the checkbox next to the group `acme-cloud-admin` or similar.
11. Select `Next: Permission sets`.
12. Select the checkbox next to `AWSAdministratorAccess`.
13. Select `Finish`.

Now you've enabled all users who are part of the Cloud Administrator group in AWS SSO administrator access to the selected AWS accounts.

## 5. Apply Names to Shared VPC Resources

Since the names of shared subnets are not currently propagated to AWS accounts, as a Cloud Administrator, you can optionally apply names to the shared subnets within each development AWS account so that it's easier for the development teams to understand the role of each subnet. For example, more readily distinguising between public and private subnets.

1. As a Cloud Administrator, use your personal user to log into AWS SSO.
2. Select the development AWS account of interest.
3. Select `Management console` associated with the **`AWSAdministratorAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to **`VPC`**.
6. Select `Your VPCs`.
7. Select the unamed VPC and assign the same name as used in the Network AWS account. For example, **`shared`**.
8. Select `Subnets`.
9. Update the `Name` field of each subnet to match the name of the subnet as it's configured in the `Network` AWS account. You can open another icognito or similar browser session to view the `Network` account's resources.

---
**Review Note: This step is ripe for automation**

See [issue 18](https://github.com/ckamps/aws-foundation-journey/issues/18)

---

## Next Steps

[7. Onboard Development Teams](2-7-onboard-dev-teams.md)
