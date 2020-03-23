# Using AWS Services in Your Development Environment

---
***DRAFT CONTENT***

Content in this repository is in a preliminary draft form and should not be used for formal build outs of AWS environments unless an AWS specialist is working with you.  

The documentation is currently undergoing frequent changes as it is reviewed and tested. See the [Change Log](../../CHANGELOG.md) for notable changes.

If you'd like to contribute to this effort via feedback, bug fixes, and/or enhancements, see [How to Contribute](../../CONTRIBUTING.md). 

---

The following documents address how developers can self-service access a variety of AWS services in their development AWS accounts.

## Special Considerations

Why do development teams need special instructions to use AWS services in their development AWS accounts?

### Use of Existing Shared Development VPC

Since your development permissions do not allow you to create VPC resources, configuration of AWS services that depend on VPC resources needs to take into account the use of an existing VPC.

### Creation of AWS Service IAM Roles

Since AWS services may require you to create AWS service specific IAM roles and your ability to create IAM roles requires that you associate the development IAM boundary policy to all roles, the process for configuring IAM service roles needs to be addressed.

Refer to [Controlling Development Team Access](../3-3-controlling-dev-team-access) for more background on permissions provided to development teams in development AWS accounts and the role of AWS IAM boundary policies.

## Developer Tools

* [AWS Cloud9 Web IDE](1-cloud9.md)

## Compute

* [Amazon Elastic Kubernetes Service (EKS)](2-eks.md)

## Database

* [Amazon Redshift](3-redshift.md)