# 7. Onboard the Initial Development Teams

In this step your Security and Cloud Admins will onboard a limited set of initial developers who will have access to their team development environment. The outcome is that a small team of developers has the knowledge to start using their AWS development account, where to find basic usage documentation, and who to contact for support.

This step should take about 60 minutes to complete.

1. [Assemble Onboarding Documentation](#1-assemble-onboarding-documentation)
2. [Create Development Team Groups in AWS SSO](#2-create-development-team-groups-in-aws-sso)
3. [Create Development Team Users in AWS SSO](#3-create-development-team-users-in-aws-sso)
4. [Enable Foundation Team Members Access Their Development AWS Account](#4-enable-foundation-team-members-access-their-development-aws-account)
5. [Brief Development Team Members](#5-brief-development-team-members)

## 1. Assemble Onboarding Documentation

Working with your cross-functional colleagues in Security, Compliance, and Finance, use the following resources to help assemble an onboarding or getting started document and share with the members of the initial development teams so that they understand the fundamentals of their responsibilities, access permissions, and how to access and begin using their development AWS accounts. 

Key aspects to cover in the onboarding documentation include:

### Their Access Permissions and Responsibilities

...

### How to Access their Team's Development AWS Account

...

#### Access Via AWS Management Console

...

#### Access Via AWS CLI, AWS SDKs, and AWS APIs

...

### How to Monitor Costs Incurred Via Their Development AWS Account

...

## 2. Create Development Team Groups in AWS SSO

Create a new group in AWS SSO for each of the development teams and associate those groups with an initial set of permissions and their respective development AWS accounts.

### Create Development Team Groups in AWS SSO

1. As a cloud administrator, use your personal user to log into AWS SSO.
2. Select the AWS master account.
3. Select `Management console` associated with the `AWSAdministratorAccess` role.
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

## 3. Create Development Team Users in AWS SSO

Now that you've established the two development oriented groups in AWS SSO and wired these groups to a set of permissions and AWS accounts, your next step is to create a user in AWS SSO for each development team member.

***...add instructions...refer to earlier section where they already added the foundation team users...***

## 4. Enable Foundation Team Members Access Their Development AWS Account

Since you've already created users in AWS SSO for foundation team members, all you need to do to enable those team members to access their development AWS account is to add the foundation team member users to the newly created group in AWS SSO.

1. Access `Groups` in AWS SSO.
2. Select `acme-foundation-dev`.
3. Select `Add users`.
4. Select the checkbox for each foundation team member.
5. Select `Add users`.

The foundation team members now have access to the foundation team development AWS account.

## 5. Brief Development Team Members

***...highlight the need to communicate the onboarding information to development team members...***

## Next Steps

[8. Managing and Monitoring Your AWS Environment](2-8-manage-and-monitor-aws-environment.md)
