# 3. Set Up Initial AWS Platform Access Controls

In this step your Security and Cloud Administrators will decide on and implement the initial approach to controlling access to the AWS platform.

This step should take about 45 minutes to complete.

1. [Temporarily Use AWS SSO Locally Managed Users and Groups](#1-temporarily-use-aws-sso-locally-managed-users-and-groups)
2. [Map Foundation Functional Roles to Existing AWS Groups](#2-map-foundation-functional-roles-to-existing-aws-groups)
3. [Access AWS SSO Using Your AWS Control Tower Administrator User](#3-access-aws-sso-using-your-aws-control-tower-administrator-user)
4. [Customize AWS SSO Portal URL](#4-customize-aws-sso-portal-url)
5. [Add a Cloud Admin Group in AWS SSO](#5-add-a-cloud-admin-group-in-aws-sso)
6. [Add a Cost Management Group and Assign Permissions in AWS SSO](#6-add-a-cost-management-group-and-assign-permissions-in-aws-sso)
7. [Create Organizational Units](#7-create-organizational-units)
8. [Distribute Permissions Boundary to Development OU](#8-distribute-permissions-boundary-to-development-ou)
9. [Create Development Team Permission Set in AWS SSO](#9-create-development-team-permission-set-in-aws-sso)
10. [Configure Multi-Factor Authentication (MFA) Requirements](#10-configure-multi-factor-authentication-mfa-requirements)

## 1. Temporarily Use AWS SSO Locally Managed Users and Groups

If your team needs to move very quickly in a matter of 1-2 days to establish an initial development environment and does not have an immediate requirement to integrate your existing enterprise identity management system to help control access to the AWS platform, then it’s recommended that:

1. Your Security and Cloud Administrators temporarily define and manage users and groups within the AWS SSO service.
2. Make plans for a parallel workstream to integrate your preferred enterprise identity management system with the AWS platform and transition away from locally managed users and groups in the AWS SSO service.

If your organization requires integration of your existing identity management system even for the establishment of an initial development environment, then see [Establishing Federated Access to AWS](../2-fast-follow-ons/2-1-federated-access-to-aws.md) before proceeding further in this guide.

---

**Note: What about AWS IAM users and groups?**

Although the AWS Identity and Access Management (AWS IAM) service supports management of locally defined users and groups, it’s generally not recommended that customers depend on this capability to help manage human user access to the AWS platform _at scale_. Instead, AWS recommends organizations integrate use of their preferred enterprise identity management system.

---

## 2. Map Foundation Functional Roles to Existing AWS Groups

Earlier in this guide you should have mapped your foundation team members to the [initial set of functional roles](1-3-map-people-to-foundation-roles.md) to be played in support of your AWS environment. 

The following table represents a mapping of those functional roles to a set of AWS SSO groups and permissions. Although AWS Control Tower automatically provisioned most of the AWS SSO groups, several of the groups in the table are not pre-defined. You will create these custom groups later in this section.

|Foundation Functional Role|AWS SSO Groups|Effective Permissions|
|---	|---	|--- |
|Cloud Administration|`AWSControlTowerAdmins`|[Administrator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html#jf_administrator) access in the master, log archive, and audit accounts.|
| |`AWSAccountFactory`|Abilty to use the Account Factory product via AWS Service Catalog.|
| |`acme-cloud-admin`|[Administrator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html#jf_administrator) access in all other AWS accounts.
|Security Administration|`AWSAuditAccountAdmins`|[Administrator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html#jf_administrator) access in the audit account.|
| |`AWSLogArchiveAdmins`|[Administrator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html#jf_administrator) access in the log archive account.|
| |`AWSSecurityAuditPowerUsers`|[Developer power user](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html#jf_developer-power-user) access across all accounts.|
|Cost Management|`acme-cost-mgmt`|[Billing and cost management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html#jf_accounts-payable) access in the master account.|
|Audit|`AWSSecurityAuditors`|Read only access in all accounts.|

---

**Note: Your AWS platform access permissions will evolve**

The initial mapping of functional roles to groups in AWS SSO and the underlying permissions associated with those groups shown in the table above is only a simple starting point for your AWS platform access permissions for foundation team members. As you progress on your journey, you will evolve these groups and underlying permissions to meet your needs.

---

## 3. Access AWS SSO Using Your AWS Control Tower Administrator User

You'll need to use the AWS SSO service to add a new groups for Cloud Administrators and Cost Managers and create users for foundation team members.

Since you have not yet created users in AWS SSO for each member of your foundation team, your Security or Cloud Administrator team members will need to use the AWS Control Tower Administrative user to start adding AWS SSO users for each foundation team member.  Once these users have been onboarded in a subsequent step, you can stop using the AWS Control Tower Administrator user.

Access the AWS SSO service:

1. Sign in to the AWS SSO URL for your environment using the **AWS Control Tower Administrator** user.
2. Select the AWS **master** account.
3. Select **`Management console`** associated with the **`AWSAdministratorAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to **`AWS SSO`**.

---

**Note: Permissions error**

If you encounter a permissions error when attempting to access AWS SSO via the AWS Management Console, ensure that you've selected the proper AWS account and role, `AWSAdministratorAccess`.

---

## 4. Customize AWS SSO Portal URL

As an optional step, you may want to customize the URL that your organization uses to access the AWS SSO portal.  

If you have plans to implement your own internal DNS alias for the portal, you can skip this step.

The default form the portal URL is similar to this example of: `https://d-3a274d5e7d.awsapps.com/start`. Via the AWS SSO settings, you can customize the `d-3a274d5e7d` portion of the URL shown in the example.

1. Access **`Groups`** in AWS SSO.
2. Select **`Settings`**.
3. Under **`User portal`**, select **`Customize`**.
4. Set the first portion of the URL to a unique value.  Use your organization identifier, stock ticker symbol, or another identier that you use as an abbreviated reference to your organization.

## 5. Add a Cloud Admin Group in AWS SSO

Since Cloud Administrators don't have administrator access to newly created AWS accounts, you'll need to start laying the groundwork for this access by adding a new group in AWS SSO. In a subsequent step, you'll add Cloud Administrator team members to the new group. Later on, after the initial set of development team AWS account are created, you will assign this group and a permission set to each of those new accounts so that the Cloud Administrators can gain administrator level access to manage those accounts. 

1. Access **`Groups`** in AWS SSO.
2. Select **`Create group`**.
3. Provide a group name. For example **`acme-cloud-admin`**. Where you should replace `acme` with a common abbreviation for your organization.
4. Provide a description. For example, **`Cloud administration`**.
5. Select **`Create`**.

---
**Note: Cloud resource naming**

**Using Qualifiers in Shared Namespaces:** When adding cloud resources to a shared namespace, it's a best practice to prefix those resource names with an organization identifier so that you avoid conflict with AWS-managed resources and can easily identify your own custom resources. 

**Lower Case, Camel Case, etc:** Most AWS cloud resource names support using a range of characters and cases.  Typically, AWS-managed resources use camelcase, but organizations often standardize on one style and strive to use that style throughout their cloud environment.

---

## 6. Add a Cost Management Group and Assign Permissions in AWS SSO

Since there's no suitable predefined AWS SSO group for cost management team members, you need to add a new group in AWS SSO and associate the necessary permissions with that group. In a subsequent step, you'll add cost management team members to the new group. 

In the spirit of least privilege access, the resulting permissions will enable cost management team members to access only your master AWS account and only the cost management and billing resources and data accessible within that AWS account.

### Add Cost Management Group in AWS SSO

1. Access **`Groups`** in AWS SSO.
2. Select **`Create group`**.
3. Provide a group name. For example **`acme-cost-mgmt`**. Where you should replace `acme` with a common abbreviation for your organization.
4. Provide a description. For example, 'Cost management and billing`.
5. Select **`Create`**.

### Associate Group and Permission Set with AWS Master Account

1. Access **`AWS accounts`** in AWS SSO.
2. Select the checkbox next to your **master** AWS account.
3. Select **`Assign users`**.
4. Select **`Groups`**.
5. Select the checkbox next to **`acme-cost-mgmt`** or similar.
6. Select **`Next: Permission sets`**.
7. Select the checkbox next to **`Billing`**.
8. Select **`Finish`**.

## 7. Create Organizational Units

Using AWS Control Tower, create several Organizational Units (OUs) that will act as a mechanism to group AWS accounts that have similar security and management needs.  Initially, the OU structure will simply consist of two custom OUs:

* **`infrastructure`** - For foundation infrastructure related AWS accounts including the Network AWS account that you will create later in this section.
* **`development`** - For development team AWS accounts that you'll create in the next section.

---
**Note: Your OU design will evolve** 

Contrary to what's implied by the name "OU", AWS Organizations OUs are not meant to be used to reflect your enterprise's organizational structure. Instead, they are intended to provide a means to group AWS accounts witn similar security and operational requirements.

Since you have the ability to move AWS accounts between OUs and modify OUs, you don't need to perform a complete OU design at this early stage. As you progress on your journey, you will evolve your OU design to suit your emerging needs.  If you'd like to learn more about OUs, see [AWS Organizations in Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/organizations.html).

---
### Create the `infrastructure` OU

1. Navigate to **`AWS Control Tower`**.
2. Select **`Organizational units`**.
3. Select **`Add an OU`**.  
4. Follow the prompts to create a new OU named **`infrastructure`**.

### Create the `development` OU

1. Create another OU named **`development`**.
2. Once the OU has been created, select the **`development`** OU and record the ID of the form **`ou-....`** so that you can use it in the next step.

## 8. Distribute Permissions Boundary to Development OU

In this step you'll use AWS CloudFormation StackSets to distribute an IAM permissions boundary policy to the "development" OU that you just created.  This boundary policy will help ensure that development teams can't modify your foundation cloud resources.

In a later section, when you create several development team AWS accounts, you will associate the AWS accounts with the "development" OU. Any AWS account that is added to that OU will automatically be configured with the IAM permissions boundary policy resource.  Similarly, when an AWS account is removed from the OU, the IAM permissions boundary policy resource will be automatically removed from the AWS account.

---
**Note: Review the sample development team access controls**

See [Controlling Development Team Access](3-3-controlling-dev-team-access.md) for a detailed explanation of the requirements and sample implementation of how you can provide freedom to your development teams in their development team AWS accounts, but inhibit them from adversely impacting the security of your overall AWS environment.

---

### Enable Trusted Access in AWS Organizations

First, enable the AWS CloudFormation service to automatically configure permissions required to use the CloudFormation StackSets feature to deploy stacks to AWS accounts in your AWS organization.

1. Navigate to **`AWS CloudFormation`**.
2. Select **`StackSets`**.
3. Select **`Enable trusted access`**.

If you'd like more background, see [Enabling Trusted Access with AWS Organizations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-orgs-enable-trusted-access.html).

### Download AWS CloudFormation Template

Next, download the sample AWS CloudFormation template [acme-base-dev-team-boundary.yml](../4-code-samples/01-iam-policies/acme-base-dev-team-boundary.yml) to your desktop.

### Deploy Permissions Boundary as a StackSet

Create a StackSet to deploy the permissions boundary policy to all AWS accounts associated with the "development" OU. 

1. Select **`Create StackSet`**.
2. Select **`Upload a template file`**.
3. Select **`Choose file`** to select the downloaded template file from your desktop.
5. Select **`Next`**.
6. Enter a **`StackSet name`**. For example, **`acme-base-dev-team-boundary`**. 

It's useful to prefix your custom cloud resources that live in a larger name space with your organization identifier and a qualifier such as **`base`** to represent foundation resources. The important consideration is to be consistent with naming of foundation cloud resources so that you can apply IAM policies that will inhibit unauthorized modification of those resources.

7. In **`Parameters`**:

|Parameter|Guidance|
|---------|--------|
|**`pOrg`**|Replace **`acme`** with your organization identifier or stock ticker if that applies. This value is used as a prefix in the name of IAM managed policy that is created by the template.|

Leave the other parameters at their default settings.

7. Select **`Next`**.
8. Leave the **`Permissions`** set to **`Service managed permissions`**.
9. Select **`Next`**.
10. In **`Deployment targets`**, select **`Deploy to organizational units (OUs)`**.
11. Enter the OU ID of the "development" OU that you created in the previous step.
12. In **`Specify regions`**, select your home AWS region.
13. Select **`Next`**.
14. Scrolls to the bottom and mark the checkbox to acknowledge that IAM resources will be created.
15. Select **`Submit`**.

Since you have not yet created the development team AWS accounts, this CloudFormation StackSet won't create CloudFormation stacks in the development team AWS accounts until those AWS accounts are created in a subsequent section.

Proceed to the next step.

## 9. Create Development Team Permission Set in AWS SSO

Next, you'll create a custom permission set in AWS SSO to represent the initial iteration of an AWS IAM policy under which development team members will work in their development AWS accounts.

### Download and Customize Sample IAM Policy

1. Download the [sample policy](../4-code-samples/01-iam-policies/acme-base-dev-team.json) to your desktop.
2. Open the file and replace all occurrences of **`aceme`** with a reference to your own organization's identifier.

---
**Note: Infrastructure as Code (IaC) Opportunity**

Since you've just modified "code" that represents an important security policy for your AWS environment, it's a best practice to manage that source code file in a version control system such as a Git-based system and control who can modify this file moving forward. If your organization is not already using Git-based version control, see the [Fast Follow-on Capabilities](../2-fast-follow-ons/) for assistance on how to get started using Git-based version control.

---

### Create Permission Set in AWS SSO

1. Access **`AWS accounts`** in AWS SSO.
2. Select **`Permission sets`**.
3. Select **`Create permission set`**.
4. Select **`Create a customer permission set`**.
5. Enter a **`Name`**. For example **`acme-base-dev-team`**. 
6. Enter a **`Description`**. For example, **`Day-to-day permission used by developers in their development AWS accounts.`**.
7. Set the **`Session duration`** to the desired value.
8. Select the checkbox **`Create a custom permissions policy`**.
9. Open the sample policy file that you just customized in a text editor, copy, and paste the content.
10. Select **`Create`**.

Later, when you onboard the development teams to their development AWS accounts, you'll reference this permission set.

## 10. Configure Multi-Factor Authentication (MFA) Requirements

Before adding any human users to AWS SSO and enabling the users to access your AWS environment, it's a best practice to configure AWS SSO to require multi-factor authentication (MFA).

In the following steps, you will modify your AWS SSO configuration to align with typical security best practices.

Follow these steps to make the MFA related changes:

1. Access **`Settings`** in AWS SSO.
2. Under **`Multifactor authentication`** select **`Configure`**.
3. Under **`Users should be prompted for multi-factor authentication (MFA)`**, select **`Every time they sign in (always-on)`**.
4. Under **`When prompted for a MFA code` select `Require them to provide a one-time password sent by email`**.
5. Under **`Who can manage MFA devices` select `Users and administrators can add and manage MFA devices`**.
6. Select **`Save changes`**.

---
**Note: Auditing use of MFA**

The configuration shown above does not force the use of MFA, but it does impose an additional overhead of a one-time password sent via email for users that have not yet registered an MFA device.

You will likely want to establish either manual or automatic recurring audits to ensure that your users have registered an MFA device.

---

## Next Steps

[4. Onboard the Foundation Team](2-4-onboard-foundation-team.md)
