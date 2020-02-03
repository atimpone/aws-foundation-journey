# 4. Set Up Initial AWS Platform Access Controls

In this step your Security and Cloud Administrators will decide on and implement the initial approach to controlling access to the AWS platform for use by users who are responsible for your cloud foundation and are members of development teams.

This initial set of access controls will evolve as your use of the AWS platform expands.

This step should take about 30 minutes to complete.

***Chris left off reviewing and editing here...***

**Decision Point: Temporarily Use AWS SSO Locally Managed Users and Groups or Integrate Existing Identity Management System**

If your team needs to move very quickly (in a matter of a day or two) to establish an initial development environment and does not have an immediate requirement to integrate its existing enterprise identity management system to help control access to the AWS platform, then it’s recommended that:

1. Your team temporarily defines and manages users and groups within the AWS SSO service.
2. In support of expanded use of AWS by more people and teams in the future, make plans in parallel to integrate your preferred enterprise identity management system with the AWS platform and transition away from locally managed users and groups in the AWS SSO service.

If you organization requires integration of your existing identity management system even for the establishment of an initial development environment, then see **Establishing Federated Access to AWS** before proceeding further in this guide.

**What about AWS IAM users and groups?**

Although the AWS IAM service supports management of locally defined users and groups, it’s generally not recommended that customers depend on this capability to help manage human user access to the AWS platform. Instead, AWS recommends organizations integrate use of their preferred enterprise identity management system.

## Review Automatically Configured Access Controls

...is this review necessary? Should we instead just highlight already configured AWS SSO groups only when they actually come into play within the context of our guidance?

Automatically created AWS SSO Groups:

* AWSAccountFactory
    * Assumes Role: Service Catalog End User Access in the AWS Master Account
* AWSServiceCatalogAdmins
    * Assumes Role: Service Catalog Admins in the AWS Master Account
* AWSControlTowerAdmins
    * Assumes Role: AWSOrganizationsFullAccess in the AWS Master Account
    * Assumes Role: AdministratorAccess in the AWS Master Account
* AWSSecurityAuditPowerUsers
    * Assumes Role: PowerUserAccess in all AWS Accounts
* AWSSecurityAuditors
    * Assumes Role: ReadOnlyAccess in all AWS Accounts
* AWSLogArchiveAdmins
    * Assumes Role: AdministratorAccess in the AWS Archive Account
* AWSLogArchiveViewers
    * Assumes Role: ReadOnlyAccess in the AWS Archive Account
* AWSAuditAccountAdmins
    * Assumes Role: AdministratorAccess in the AWS Audit Account


**CREATE INITIAL SET OF USERS**
[AWS SSO User Guide](https://docs.aws.amazon.com/controltower/latest/userguide/sso.html)
[How to add a user in AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/addusers.html)

**ADD USERS TO BUILD IN CONTROL TOWER GROUPS**
[How to add users to groups](https://docs.aws.amazon.com/singlesignon/latest/userguide/adduserstogroups.html)

## Enable Multi-Factor Authentication (MFA)

...as a best practice, even for the initial stage of experimentation and early development, enable Multi-factor Authentication (MFA) requirements in AWS SSO... provide recommended settings for this section of the AWS SSO Settings:
[Image: image.png]Question: How does the customer enforce that MFA via AWS SSO has been configured for all users? i.e. to enable self-service, presumably we’d allow users to sign in without MFA so that they can set up their MFA. But what mechanism can be used to ensure that users eventually set up MFA?

[How to setup MFA](https://docs.aws.amazon.com/singlesignon/latest/userguide//enable-mfa.html)