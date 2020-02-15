# 4. Set Up Initial AWS Platform Access

In this step your Security and Cloud Administrators will decide on and implement the initial approach to controlling access to the AWS platform and onboard the foundation team members with the appropriate permissions so that they can begin to access your AWS environment.

This step should take about 45 minutes to complete.

1. Temporarily Use AWS SSO Locally Managed Users and Groups
2. Map Foundation Functional Roles to Existing AWS Groups
3. Access AWS SSO Using Your AWS Control Tower Administrator User
4. Add a Cost Management Group and Permissions in AWS SSO
5. Enable Multi-Factor Authentication (MFA)
6. Create AWS SSO Users for Foundation Team Users
7. Onboard Your Foundation Team Members
8. Stop Using the AWS Control Tower Administrative User

## 1. Temporarily Use AWS SSO Locally Managed Users and Groups

If your team needs to move very quickly in a matter of 1-2 days to establish an initial development environment and does not have an immediate requirement to integrate your existing enterprise identity management system to help control access to the AWS platform, then it’s recommended that:

1. Your Security and Cloud Administrators temporarily define and manage users and groups within the AWS SSO service.
2. Make plans for a parallel workstream to integrate your preferred enterprise identity management system with the AWS platform and transition away from locally managed users and groups in the AWS SSO service.

If your organization requires integration of your existing identity management system even for the establishment of an initial development environment, then see [Establishing Federated Access to AWS](../2-fast-follow-on/2-1-federated-access-to-aws.md) before proceeding further in this guide.

---

**Note: What about AWS IAM users and groups?**

Although the AWS Identity and Access Management (AWS IAM) service supports management of locally defined users and groups, it’s generally not recommended that customers depend on this capability to help manage human user access to the AWS platform. Instead, AWS recommends organizations integrate use of their preferred enterprise identity management system.

---

## 2. Map Foundation Functional Roles to Existing AWS Groups

Earlier in this guide, you should have mapped your foundation team members to the [initial set of functional roles](2-1-map-people-to-foundation-roles.md) to be played in support of your AWS environment. The following table shows a mapping of those functional roles to a set of pre-defined AWS SSO groups and permissions.

To Do: Provide a link to where the customer can learn more about the permissions provided with each AWS SSO group.

|Foundation Functional Role|AWS SSO Groups|
|---	|---	|
|Cloud Administration|`AWSControlTowerAdmins`<br>`AWSAccountFactory`|
|Security Administration|`AWSAuditAccountAdmins`<br>`AWSLogArchiveAdmins`<br>`AWSSecurityAuditPowerUsers`|
|Cost Management|`acme-cost-mgmt` (to be added later in this section)|
|Audit|`AWSSecurityAuditors`|

---

**Note: Your AWS platform access permissions will evolve**

The initial mapping of functional roles to groups in AWS SSO and the underlying permissions associated with those groups shown in the table above is only a simple starting point for your AWS platform access permissions for foundation team members. As you progress on your journey, you will evolve these groups and underlying permissions to meet your needs.

---

## 3. Access AWS SSO Using Your AWS Control Tower Administrator User

You'll need to use the AWS SSO service to add a new group for cost management and create users for each foundation team members.

Since you have not yet created users in AWS SSO for each member of your foundation team, your Security or Cloud Administrator team members will need to use the AWS Control Tower Administrative User to start adding AWS SSO users for each foundation team member.  Ensure that you have the email address and login credentials for this user before continuing.

Access the AWS SSO service:

1. Sign in to the AWS SSO URL for your environment using the AWS Control Tower Administrator user.
2. Select the AWS master account.
3. Select `Management console` associated with the `AWSAdministratorAccess` role.
4. Select the appropriate AWS region.
5. Navigate to `AWS SSO`.

---

**Note: Permissions error**

If you encounter a permissions error when attempting to access AWS SSO via the AWS Management Console, ensure that you've selected the proper AWS account and role, `AWSAdministratorAccess`.

---

## 4. Add a Cost Management Group and Permissions in AWS SSO

In order to fill the gap of a dedicated AWS SSO group for your cost management team members, you'll add a new group in AWS SSO and associate the necessary permissions with that group. In a subsequent step, you'll add cost management team members to the new group. 

In the spirit of least privilege access, the resulting permissions will enable cost management team members to access only your master AWS account and only the cost management and billing resources and data accessible within that AWS account.

### Add Cost Management Group in AWS SSO

1. Access `Groups` in AWS SSO.
2. Select `Create group`.
3. Provide a group name. For example `acme-cost-mgmt`. Where you should replace `acme` with a common abbreviation for your organization.
4. Provide a description. For example, 'Cost management and billing`.
5. Select `Create`.

---
**Note: Cloud resource naming**

**Using Qualifiers in Shared Namespaces:** When adding cloud resources to a shared namespace, it's a best practice to prefix those resource names with an organization identifier so that you avoid conflict with AWS-managed resources and can easily identify your own custom resources. 

**Lower Case, Camel Case, etc:** Most AWS cloud resource names support using a range of characters and cases.  Typically, AWS-managed resources use camelcase, but organizations often standardize on one style and strive to use that throughout.

TO DO: Provide link to cloud resource naming best practices.

---

### Add Permission Sets in AWS SSO

Next, we'll create the necessary permissions sets and associate them with the new group.

1. Access `AWS accounts` in AWS SSO.
2. Select the `Permission sets` tab.
3. Select `Create permission set`.
4. Select `Create a custom permission set`.
5. Provide a Name of `acme-cost-mgmt`.
6. Select `Attach AWS managed policies`. A predefined set of AWS-managed IAM permissions will be listed. In some cases, you will want to reuse these IAM-managed permissions so that you defer to AWS to keep common sets of permissiop to date. In other cases, you will create your own custom permissions.
7. Search on `Billing` and select `Billing`.
6. Select `Create`.

Now that you've created a permission set, you need to associate the permission set with the relevant AWS account and group in AWS SSO.

### Associate Group and Permission Set with AWS Master Account

1. Access `AWS accounts` in AWS SSO.
2. Select the checkbox next to your master AWS account.
3. Select `Assgn users`.
4. Select `Groups`.
5. Select the checkbox next to `acme-cost-mgmt` or similar.
6. Select `Next: Permission sets`.
7. Select the checkbox next to `acme-cost-mgmt` or similar.
8. Select `Finish`.

## 5. Enable Multi-Factor Authentication (MFA)

Before adding any human users to AWS SSO and enabling the users to access your AWS environment, it's a best practice to configure AWS SSO to require multi-factor authentication (MFA).

In the following steps, you will modify your AWS SSO configuration to:

* Enable users to authenticate via their MFA device each time they log in via AWS SSO.
* Require users to use a one-time password when they don't already have an MFA device registered. This setting will enable new users to access the AWS SSO service at least once so that they can add an MFA device.
* Enable users to add and manage their MFA devices.

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

## 6. Create AWS SSO Users for Foundation Team Users

In prepartion for adding foundation team users to AWS SSO, decide on the format of the user name.  Typically, the user name will simply be the user's corporate email address that is often used for SaaS services.

Next, access the AWS SSO service to begin adding an AWS SSO user for each foundation team member:

1. Access `Users` in AWS SSO.
2. Select `Add user`.
4. Specify a user name and complete at least the other required fields.
5. Select `Next: Groups`.
6. Using the table shown above, select the applicable groups for each user.
7. Select `Add user`.

## 7. Onboard Your Foundation Team Members 

Reach out to each foundation team member to inform them of the context of the email message they received, what they should do next, and what access they have been granted.

Their initial sign on experience will consist of:

1. Receiving the email invitation to the AWS SSO service.
1. Clicking on the `Accept invitation` link to set their initial password.
3. Being directed to AWS SSO landing page where they can select from the set of AWS accounts for which they have access.
4. Selecting from the permissions that they can assume for each AWS account.
5. Using either the AWS Management Console or AWS CLI/API to access each AWS account.

Inform the foundation team members that use of MFA is required and how they can [register an MFA device](https://docs.aws.amazon.com/singlesignon/latest/userguide/how-to-register-device.html) on their own via the AWS SSO service.

## 8. Stop Using the AWS Control Tower Administrative User

Since you've onboarded foundation team members with the appropriate permissions, as a security and compliance best practice, there's no longer any reason for your Cloud Administrators to use the AWS Control Tower Administrator user. From this point forward, the vast majority of your work to administer and manage your AWS environment should be done via your personal users that are defined in AWS SSO.  By using personal users, all operations will be auditable and tied to specific individuals.

## Next Steps

[5. Create the Initial Team Development Environments](2-5-create-team-dev-environments.md)
