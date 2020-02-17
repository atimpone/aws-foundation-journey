# 4. Set Up Initial AWS Platform Access Controls

In this step your Security and Cloud Administrators will decide on and implement the initial approach to controlling access to the AWS platform and onboard the foundation team members with the appropriate permissions so that they can begin to access your AWS environment.

This step should take about 45 minutes to complete.

1. [Temporarily Use AWS SSO Locally Managed Users and Groups](#1-temporarily-use-aws-sso-locally-managed-users-and-groups)
2. [Map Foundation Functional Roles to Existing AWS Groups](#2-map-foundation-functional-roles-to-existing-aws-groups)
3. [Access AWS SSO Using Your AWS Control Tower Administrator User](#3-access-aws-sso-using-your-aws-control-tower-administrator-user)
4. [Add a Cloud Admin Group in AWS SSO](#4-add-a-cloud-admin-group-in-aws-sso)
5. [Add a Cost Management Group and Assign Permissions in AWS SSO](#5-add-a-cost-management-group-and-assign-permissions-in-aws-sso)
6. [Configure Multi-Factor Authentication (MFA) Requirements](#6-configure-multi-factor-authentication-mfa-requirements)

## 1. Temporarily Use AWS SSO Locally Managed Users and Groups

If your team needs to move very quickly in a matter of 1-2 days to establish an initial development environment and does not have an immediate requirement to integrate your existing enterprise identity management system to help control access to the AWS platform, then it’s recommended that:

1. Your Security and Cloud Administrators temporarily define and manage users and groups within the AWS SSO service.
2. Make plans for a parallel workstream to integrate your preferred enterprise identity management system with the AWS platform and transition away from locally managed users and groups in the AWS SSO service.

If your organization requires integration of your existing identity management system even for the establishment of an initial development environment, then see [Establishing Federated Access to AWS](../2-fast-follow-on/2-1-federated-access-to-aws.md) before proceeding further in this guide.

---

**Note: What about AWS IAM users and groups?**

Although the AWS Identity and Access Management (AWS IAM) service supports management of locally defined users and groups, it’s generally not recommended that customers depend on this capability to help manage human user access to the AWS platform _at scale_. Instead, AWS recommends organizations integrate use of their preferred enterprise identity management system.

---

## 2. Map Foundation Functional Roles to Existing AWS Groups

Earlier in this guide you should have mapped your foundation team members to the [initial set of functional roles](2-1-map-people-to-foundation-roles.md) to be played in support of your AWS environment. 

The following table represents a mapping of those functional roles to a set of AWS SSO groups and permissions. Although AWS Control Tower automaitcally provisioned most of the AWS SSO groups, several of the groups in the table are not pre-defined. You will create these custom groups later in this section.

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

You'll need to use the AWS SSO service to add a new group for cost management and create users for each foundation team members.

Since you have not yet created users in AWS SSO for each member of your foundation team, your Security or Cloud Administrator team members will need to use the AWS Control Tower Administrative User to start adding AWS SSO users for each foundation team member.  Ensure that you have the email address and login credentials for this user before continuing.

Access the AWS SSO service:

1. Sign in to the AWS SSO URL for your environment using the AWS Control Tower Administrator user.
2. Select the AWS **master** account.
3. Select `Management console` associated with the **`AWSAdministratorAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to `AWS SSO`.

---

**Note: Permissions error**

If you encounter a permissions error when attempting to access AWS SSO via the AWS Management Console, ensure that you've selected the proper AWS account and role, `AWSAdministratorAccess`.

---

## 4. Add a Cloud Admin Group in AWS SSO

Since Cloud Administrators don't have administrator access to newly created AWS accounts, you'll need to start laying the groundwork for this access by adding a new group in AWS SSO. In a subsequent step, you'll add Cloud Administrator team members to the new group. Later on, after the initial set of development team AWS account are created, you will assign this group and a permission set to each of those new accounts so that the Cloud Administrators can gain administrator level access to manage those accounts. 

1. Access `Groups` in AWS SSO.
2. Select `Create group`.
3. Provide a group name. For example `acme-cloud-admin`. Where you should replace `acme` with a common abbreviation for your organization.
4. Provide a description. For example, `Cloud administration`.
5. Select `Create`.

---
**Note: Cloud resource naming**

**Using Qualifiers in Shared Namespaces:** When adding cloud resources to a shared namespace, it's a best practice to prefix those resource names with an organization identifier so that you avoid conflict with AWS-managed resources and can easily identify your own custom resources. 

**Lower Case, Camel Case, etc:** Most AWS cloud resource names support using a range of characters and cases.  Typically, AWS-managed resources use camelcase, but organizations often standardize on one style and strive to use that style throughout their cloud environment.

---

## 5. Add a Cost Management Group and Assign Permissions in AWS SSO

In order to fill a gap of a dedicated AWS SSO group for your cost management team members, you need to add a new group in AWS SSO and associate the necessary permissions with that group. In a subsequent step, you'll add cost management team members to the new group. 

In the spirit of least privilege access, the resulting permissions will enable cost management team members to access only your master AWS account and only the cost management and billing resources and data accessible within that AWS account.

### Add Cost Management Group in AWS SSO

1. Access `Groups` in AWS SSO.
2. Select `Create group`.
3. Provide a group name. For example `acme-cost-mgmt`. Where you should replace `acme` with a common abbreviation for your organization.
4. Provide a description. For example, 'Cost management and billing`.
5. Select `Create`.

### Associate Group and Permission Set with AWS Master Account

1. Access `AWS accounts` in AWS SSO.
2. Select the checkbox next to your **master** AWS account.
3. Select `Assign users`.
4. Select `Groups`.
5. Select the checkbox next to `acme-cost-mgmt` or similar.
6. Select `Next: Permission sets`.
7. Select the checkbox next to `Billing`.
8. Select `Finish`.

## 6. Configure Multi-Factor Authentication (MFA) Requirements

Before adding any human users to AWS SSO and enabling the users to access your AWS environment, it's a best practice to configure AWS SSO to require multi-factor authentication (MFA).

In the following steps, you will modify your AWS SSO configuration to align with typical security best practices.

Follow these steps to make the MFA related changes:

1. Access `Settings` in AWS SSO.
2. Under `Multifactor authentication` select `Configure`.
3. Under `Users should be prompted for multi-factor authentication (MFA)`, select `Every time they sign in (always-on)`.
4. Under `When prompted for a MFA code` select `Require them to provide a one-time password sent by email`.
5. Under `Who can manage MFA devices` select `Users and administrators can add and manage MFA devices`.
6. Select `Save changes`.

---
**Note: Auditing use of MFA**

The configuration shown above does not force the use of MFA, but it does impose an additional overhead of a one-time password sent via email for users that have not yet registered an MFA device.

You will likely want to establish either manual or automatic recurring audits to ensure that your users have registered an MFA device.

---

## Next Steps

[5. Onboard the Foundation Team](2-5-onboard-foundation-team.md)
