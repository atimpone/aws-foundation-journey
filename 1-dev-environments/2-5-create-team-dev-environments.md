# 5. Create the Initial Team Development Environments

In this step your Cloud Administrators will create several new team development AWS accounts via AWS Control Tower's Account Factory.

This step should take about 30 minutes to complete.

## 1. Use at Least Two Development AWS Accounts from the Start

As highlighted previously, an AWS best practice is to isolate the work of distinct development teams by assigning a different AWS account for each team. Benefits of this approach include:
* Since AWS resource costs are, by default, attributable to each AWS account in which the resources are provisioned, at this early stage in your adoption, you don't need to force development teams to use cost allocation tags on their resources.

* Since cloud resources managed by development teams using different AWS accounts are, by default, completely isolated from each other, complicated AWS Identity and Access Management (IAM) configurations are not needed to ensure that development teams don't inadvertently impact each other's cloud resources.

Initially, you will likely need at least two AWS accounts for the following teams:

1. **Application Development Team** - A development AWS account for the initial application or data services development team.

2. **Cloud Administrator Team** - A development AWS account for the initial few cloud administrators to experiment, develop, and perform early testing of changes to the foundation.

## 2. Create the Development Organizational Unit

Moving forward, your company will likely want to apply particular policies or guardrails that apply to all AWS development accounts within your enterprise.  To enable you to easily target such policies across all development AWS accounts, it's recommended that you create a new Organizational Unit (OU) to represent development AWS accounts.

Within the AWS Control Tower dashboard select “Add organizational units”.  Proceed to follow the prompts to create a new OU named “development”.

In the next section when you create the new development AWS accounts, you'll specify this new OU.

You can learn more about [AWS Organizations in Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/organizations.html).

## 3. Create Development Account

In AWS Control Tower, provision an initial AWS team development account for early experimentation, development, and testing.  You may need to repeat this step, and the following related permissions steps in order to complete the provisioning of all your accounts.

The accounts you provision from account factory shouldn’t be considered permanent.  Nearly every part of an AWS account (outside the account’s primary email address) can be changed and updated at a later date.  With the OU structure in place from earlier in the guide, you can be confident that large changes can be quickly made to all child accounts should the need rise.

See [How to deploy an AWS account with Account Factory](https://docs.aws.amazon.com/controltower/latest/userguide/account-factory.html#configure-provision-new-account) to set up the initial development team accounts. 

## 4. Set Up Baseline Access Permissions

After the initial team development account is created via AWS Control Tower, establish an initial set of baseline access into those accounts following these steps:

1. **Login to the AWS Master Account**
2. **Create Users in AWS SSO that require access to the Development account
    **[**How to add a user in AWS SSO**](https://docs.aws.amazon.com/singlesignon/latest/userguide/addusers.html)
3. **Create the following AWS SSO Groups for Development use
    **[**How to add AWS SSO Groups**](https://docs.aws.amazon.com/singlesignon/latest/userguide/addgroups.html)** **
    1. ACMETeamADevGroup
        1. AWSPowerUsers
    2. ACMEFoundationsDevGroup
        1. AWSPowerUsers
4. **Add Groups to the AWS Development Account**
5. **Add Permission Sets to each group**
6. **Add users to the group with the required permission sets**


Finally, you can inform newly added users that they should configure MFA for their user accounts and provide instructions on how to do so via the AWS SSO User Portal.

[AWS SSO - Enable Multi-Factor Authentication](https://docs.aws.amazon.com/singlesignon/latest/userguide/enable-mfa.html)

For a more prescriptive approach on how to onboard team members into their new AWS environment, see Appendix A

## Next Steps

[6. Establish Initial AWS Platform Monitoring Practices](2-6-initial-aws-platform-monitoring.md)
