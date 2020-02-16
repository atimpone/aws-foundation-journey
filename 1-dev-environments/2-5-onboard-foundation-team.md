# 5. Onboard Foundation Team

In this step your Cloud Administrators will onboard the few people that make up the initial foundation team so that they can stop using system users and start using their own user accounts to manage the foundation.

This step should take about 20 minutes to complete.

1. [Create AWS SSO Users for Foundation Team Users](#1-create-aws-sso-users-for-foundation-team-users)
2. [Onboard Your Foundation Team Members](#2-onboard-your-foundation-team-members)
3. [Stop Using the AWS Control Tower Administrative User](#3-stop-using-the-aws-control-tower-administrative-user)

## 1. Create AWS SSO Users for Foundation Team Users

In prepartion for adding foundation team users to AWS SSO, decide on the format of the user name.  Typically, the user name will simply be the user's corporate email address that is often used for SaaS services.

Next, access the AWS SSO service to begin adding an AWS SSO user for each foundation team member:

1. Access `Users` in AWS SSO.
2. Select `Add user`.
4. Specify a user name and complete at least the other required fields.
5. Select `Next: Groups`.
6. Using the table shown above, select the applicable groups for each user.
7. Select `Add user`.

## 2. Onboard Your Foundation Team Members 

Reach out to each foundation team member to inform them of the context of the email message they received, what they should do next, and what access they have been granted.

Their initial sign on experience will consist of:

1. Receiving the email invitation to the AWS SSO service.
1. Clicking on the `Accept invitation` link to set their initial password.
3. Being directed to AWS SSO landing page where they can select from the set of AWS accounts for which they have access.
4. Selecting from the permissions that they can assume for each AWS account.
5. Using either the AWS Management Console or AWS CLI/API to access each AWS account.

Inform the foundation team members that use of MFA is required and how they can [register an MFA device](https://docs.aws.amazon.com/singlesignon/latest/userguide/how-to-register-device.html) on their own via the AWS SSO service.

## 3. Stop Using the AWS Control Tower Administrative User

Since you've onboarded foundation team members with the appropriate permissions, as a security and compliance best practice, there's no longer any reason for your Cloud Administrators to use the AWS Control Tower Administrator user. 

From this point forward, the vast majority of your work to administer and manage your AWS environment should be done via your personal users that are defined in AWS SSO.  By using personal users, all operations will be auditable and tied to specific individuals.

## Next Steps

[6. Determine Initial Networking Approach](2-6-determine-networking-approach.md)