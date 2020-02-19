# 7. Onboard Initial Development Teams

In this step either Security or Cloud Administrators will onboard a limited set of initial developers who will have access to their team development environment. The outcome is that a small team of developers has the knowledge to start using their AWS development account, where to find basic usage documentation, and who to contact for support.

This step should take about 60 minutes to complete.

1. [Assemble Onboarding Documentation](#1-assemble-onboarding-documentation)
2. [Create Development Team Groups in AWS SSO](#2-create-development-team-groups-in-aws-sso)
3. [Create Development Team Users in AWS SSO](#3-create-development-team-users-in-aws-sso)
4. [Enable Foundation Team Members Access to Their Development AWS Account](#4-enable-foundation-team-members-access-their-development-aws-account)
5. [Brief Development Team Members](#5-brief-development-team-members)

## 1. Assemble Onboarding Documentation

Work with your cross-functional colleagues in Security, Compliance, and Finance to assemble the basic form of a getting started document and share with the members of the initial development teams so that they understand the fundamentals of their responsibilities, access permissions, and how to access and begin using their development AWS accounts. 

See the [Example Getting Started Guide](3-2-getting-started-guide-dev-teams.md) as a recommended starting point.

## 2. Create Development Team Groups in AWS SSO

Create a new group in AWS SSO for each of the development teams and associate those groups with an initial set of permissions and their respective development AWS accounts.

### Create Development Team Groups in AWS SSO

1. As a Cloud Administrator, use your personal user to log into AWS SSO.
2. Select the AWS **master** account.
3. Select `Management console` associated with the **`AWSAdministratorAccess`** role.
4. Select the appropriate AWS region.
5. Navigate to AWS SSO.
6. Access `Groups` in AWS SSO.
7. Select `Create group`.
8. Provide a group name. For example, replacing `acme` with your organization's identifier:
  * `acme-team-a-dev`
  * `acme-foundation-dev`
9. Provide a description. For example:
  * `Team A development`
  * `Foundation team development`
10. Select `Create`.

### Associate Groups with Permissions and Development AWS Accounts

1. Access `AWS accounts` in AWS SSO.
2. Select the checkbox next to the development AWS account of interest. For example:
  * `Team A - Dev`
  * `Foundation - Dev`
3. Select `Assgn users`.
4. Select `Groups`.
5. Select the checkbox next to the group of interest. For example:
  * `acme-team-a-dev`
  * `acme-foundation-dev`
6. Select `Next: Permission sets`.
7. Select the checkbox next to `AWSPowerUserAccess`.
8. Select `Finish`.

Repeat the process above to create a group for your foundation team and enable this group to access their development AWS account.

---
**Note: `AWSPowerUserAccess` permissions**

As a getting started step, this guide suggests using one of the pre-defined, AWS-managed permission sets for your development team users and their access to their development AWS accounts. However, you will likely define your own custom set of permissions in AWS IAM to meet your business and security needs and supplant the initial permission set.

---

---
**Review Note: Power user access might be insufficient**

We need to validate that the predefined AWS managed permission is sufficient as a starting point. It has some restrictions that might not be compatible with common dev use cases.

Indeed, it is not sufficient. See [Issue 15](https://github.com/ckamps/aws-foundation-journey/issues/15)

---

## 3. Create Development Team Users in AWS SSO

Now that you've established the two development oriented groups in AWS SSO and wired these groups to a set of permissions and AWS accounts, your next step is to create a user in AWS SSO for each development team member.

Typically, the user name will simply be the user's corporate email address that is often used for SaaS services.

Next, access the AWS SSO service to begin adding an AWS SSO user for each foundation team member:

1. Access `Users` in AWS SSO.
2. Select `Add user`.
4. Specify a user name and complete at least the other required fields.
5. Select `Next: Groups`.
6. Select `acme-team-a-dev` or similar.
7. Select `Add user`.

## 4. Enable Foundation Team Members Access to Their Development AWS Account

Since you've already created users in AWS SSO for foundation team members, all you need to do to at this stage is to add the foundation team member users to the newly created foundation development group in AWS SSO.

1. Access `Groups` in AWS SSO.
2. Select `acme-foundation-dev`.
3. Select `Add users`.
4. Select the checkbox for each foundation team member.
5. Select `Add users`.

The foundation team members now have access to the foundation team development AWS account.

## 5. Brief Development Team Members

Meet with the development team members to brief them on their access and other topics covered in the  [Example Getting Started Guide](3-2-getting-started-guide-dev-teams.md). 

## Next Steps

[8. Manage and Monitor Your AWS Environment](2-8-manage-and-monitor-aws-environment.md)