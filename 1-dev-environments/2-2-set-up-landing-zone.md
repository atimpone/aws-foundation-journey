# 2. Set Up Initial Landing Zone Using AWS Control Tower

In this step your Cloud Administrators will use the AWS Control Tower service in your new AWS master account to establish an initial “landing zone” or a foundation of security guardrails and other resources that will help your organization manage use of the AWS platform. You can learn more by reviewing [AWS Control Tower Features](https://aws.amazon.com/controltower/features/).

This step should take about 90 minutes to complete.

1. [Identify Your Preferred AWS Region](#1-identify-your-preferred-aws-region)
2. [Log In as Administrator IAM User](#2-log-in-as-administrator-iam-user)
3. [Create Landing Zone Using AWS Control Tower](#3-create-landing-zone-using-aws-control-tower)
4. [Set AWS Account Root User Password and Enable MFA](#4-set-aws-account-root-user-password-and-enable-mfa)
5. [Enable MFA via AWS SSO for the Admin User Created via Control Tower](#5-enable-mfa-via-aws-sso-for-the-admin-user-created-via-control-tower)
6. [Review AWS Control Tower Best Practices for Administrators](#6-review-aws-control-tower-best-practices-for-administrators)

## 1. Identify Your Preferred AWS Region

Since AWS Control Tower will establish a set of management resources in a “home” AWS region, you need to identify which AWS region you expect to host most of your AWS management resources. You will select this region in the next step.

## 2. Log In as Administrator IAM User

Log in as the Administrator IAM user that you created in the last section before you use AWS Control Tower to set up your initial landing zone.

## 3. Create Landing Zone Using AWS Control Tower

Before using AWS Control Tower to create an initial landing zone, ensure that you review these considerations:

* **Desired Home AWS Region** - Ensure that you select the proper AWS region in the upper right hand side of the AWS Management Console before creating the landing zone. The AWS region you select should be the AWS region in which you expect do perform the majority of your work with AWS and from which you will maintain your foundation.
* **Email Distribution Lists** - Consult the [set of AWS account root user email addresses](1-4-address-pre-requisites.md#1-create-email-addresses-for-new-aws-accounts) that you established earlier.
* **Pre-Launch Checks** - Since you’ve just created a new master AWS account, the pre-launch check considerations for creating your landing zone should already be met.

Follow the steps in [Getting Started with AWS Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/getting-started-with-control-tower.html) to set up your landing zone. 

The set up process can take 20-60 minutes to complete.

## 4. Set AWS Account Root User Password and Enable MFA

Since AWS Control Tower creates two new member accounts while setting up the initial landing zone, you should follow AWS security best practices by setting the password and enabling MFA for the root user of each of the following accounts:

* Audit
* Log archive

See [Log In as Root User](https://docs.aws.amazon.com/controltower/latest/userguide/best-practices.html#root-login) in the AWS Control Tower documentation for instructions to set the root user’s password.

See [Enable MFA on the AWS Account Root User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_mfa) for instructions to enable MFA.

## 5. Enable MFA via AWS SSO for the Admin User Created via Control Tower

As part of the landing zone set up, AWS Control Tower creates a Control Tower Administrator user in the AWS Single-Sign On ( AWS SSO) service in your master account.  As a best practice, you should enable MFA for this user.

### Accept Invitation for this User

The email address associated with the AWS master account’s root user will receive an email message containing an invite to activate this user account.  Review the invitation and accept it.

<img src="../images/accept-aws-sso-invitation.png" alt="Accept SSO Invitation" width="400"/>

The email message you recieved also contains a User portal URL that you should bookmar given that it represents the URL to use SSO to access your new AWS environment., we will use it to access the AWS environment throughout the labs.

### Set Password and Activate MFA for the User

On selecting Accept Invitation, you will be redirected to the AWS Single Sign-On page and from where you could set New Password to your master account. Repeat Password and Update User to proceed.

Follow the instruction in [How to Register a Device for Use with Multi-Factor Authentication](https://docs.aws.amazon.com/singlesignon/latest/userguide/user-device-registration.html).

### Receive and Process AWS Organizations Email Message

You will receive one more email with subject AWS Organizations email verification request to the master account email address. Click on Verify your email address to continue with inviting newly created accounts into AWS Organization.

### Receive and Process AWS Notification Email Messages for Each Region

The email address you provided for the audit account will receive AWS Notification - Subscription Confirmation emails from every AWS Region supported by AWS Control Tower. To receive compliance emails in your audit account, you must choose the Confirm subscription link within each email from each AWS Region supported by AWS Control Tower.

## 6. Review AWS Control Tower Best Practices for Administrators

Now that you've set up your initial landing zone, take a few minutes to review [Best Practices for Account Administrators](https://docs.aws.amazon.com/controltower/latest/userguide/best-practices.html#tips-for-admin-maint) so that you understand temporary limitations and other considerations when working with AWS Control Tower.

For example:

* **Managing Organizational Units (OUs)** - AWS Control Tower currently supports only a single level of AWS Organizations Organizational Units (OUs) and creation of OUs to be used with AWS accounts managed by AWS Control Tower must be performed via AWS Control Tower and not via AWS Organizations.
* **Modification of AWS Account Root User Email Addresses** - AWS Control Tower does not currently support self-service modification of the email addresses associated with the root user of each AWS account.  You currently need to contact AWS Support to have these email addresses changed.

 ## Next Steps
[3. Set Up Initial AWS Platform Access Controls](2-3-set-up-aws-platform-access-controls.md)
