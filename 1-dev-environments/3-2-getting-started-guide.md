# Getting Started Guide for Development Teams

This document represents an example that can help your organization develop and publish internally your own getting started guide for teams that are onboarding to your AWS environment.  You are free to copy this content into your own internal wiki or other system and modify it to meet your needs.

As your organization progresses on its cloud adoption journey, you will likely significantly expand your internal documentation to help communicate additional and increasingly sophisticated capabilities and associated best practices that are available to teams.

---
***Review Note: Help add useful day 1 topics for new dev teams and members***

What is the minimum knowledge a dev team would need for day 1 use of their new development AWS account?

----

*...add TOC later on once the initial set of topics settles down...*

## Get Access to your AWS Account
You should've received an email from AWS with the subject "Invitation to join AWS Single Sign-On".  To login to your AWS account, you'll need to [accept the invitation](https://docs.aws.amazon.com/singlesignon/latest/userguide/howtoactivateaccount.html).

Once you're able to login, you'll need to [register an MFA device](https://docs.aws.amazon.com/singlesignon/latest/userguide/user-device-registration.html) to your AWS SSO account.


## Overview of the Cloud Environment

*...show a representaive diagram of the overall environment...*

## AWS Fundamentals
The following are some basic terms and definitions and why they're needed.

**1. What is an AWS Account?**
An AWS account is a logical container and boundary to separate AWS resources based on a number of criteria including our SLDC environment, security requirements, cost reporting, and organizational ownership.

**2. What AWS account do I have access to?**
When you log into your AWS SSO portal ([add your company's link here]()), you'll be shown a list of AWS accounts you have access to.  Initially, each development team is provided a single development AWS account.

If your team has more environment or security specific requirements please work with your cloud foundations team.

**3. If I already have an AWS account registered with my corporate/company email, can I use it instead?**
If you have production workloads, please contact your cloud foundations team to absorb that account into our proper environment to ensure compliance and security requirements are met.

For additional getting started material, based on your role, refer to the following links:
* [AWS Getting Started](https://aws.amazon.com/getting-started/)
* [AWS Training and Certification](https://aws.amazon.com/training/?e=gs&p=gsrc)
* [Start Developing with AWS](https://aws.amazon.com/developers/getting-started/)


## Initial Networking Environment

*...highlight that the initial development environment network environments will likely be supplanted over time as on-premises integration and the need to use non-overlapping IP address ranges and other enhancements emerge...*

### How to Consume Another Team's APIs or Resources

*... Connectivity options ...probably not a super high priority given that the initial context is where the customer is focusing on one or several workloads in this project stage...i.e. might not be very many teams in play at the start...but sharing services across dev teams is another reason to move soon/fast follow-on to either a shared dev VPC or using TGW to help provide relatively open connectivity across separate dev VPCs (I vote for the former at least for dev AWS accounts)...* 

## Your Access Permissions and Responsibilities

*...use of personal users set up in AWS SSO...*

*...summary of access permissions to their team's development AWS account... withe pointers to detailed permissions...*

*...extent of AWS services available via their development AWS accounts and how that extent may likely evolve over time as the security baselines get more sophisticated...*

*mention that an initial set of preventative and detective security guardrails are in place to avoid and recognize out of compliant resources...*

*highlight that their access permissions will likely be further constrained for their development AWS accounts over time to help reduce the risk to the overall organization...*

*...use scripted builds for their cloud resources where feasible to avoid cost of rework as their development AWS networks are likely to be replaced over time... provide pointers to Infrastructure as Code resources...*

## How to Access Your Team's Development AWS Account
For non-production environments, our company allows console access to create and update AWS resources.  As workloads move towards production and our practices on AWS mature, we'll be implementing a "Console Read Only" policy in production environments.

Any production workloads should be managed with infrastructure as code.

### Access Via AWS Management Console
When you log into your AWS SSO portal ([add your company's link here]()), you'll be shown a list of AWS accounts you have access to.  Initially, each development team is provided a single development AWS account.

### (Recommended) Access Via AWS CLI, AWS SDKs, and AWS APIs

AWS SSO supports CLI access.  Refer to [the official AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) to install and configure the CLI.

For a list of tools and SDKs that AWS supports, please review [Tools on AWS](https://aws.amazon.com/tools/).

## How to Monitor Costs
With our adoption of AWS, we're shifting our operation model to empower builders with more flexibility and control over their environments.  This includes understanding the AWS resources they're consuming and the costs that are associated with them.

*...reiterate their responsibility and highlight how they can monitor their costs...*

*...can teams set their own budgets? what access would they need?...*

*...provide links to existing resources to learn more...*

## How to Get an Application to Production

*.... Well Architected Review...Any other changes to traditional SDLC...*

## How to Apply Additional Compliance Guardrails for Sensitive Applications?
*... engaging cloud foundations team for SCP/Organizational changes/creation...*

## How to Learn More About AWS Services and Best Pratices

...

## How to Get Support

*...address how development teams get support to get things done in their development AWS accounts... include: 1) organization-specific support needds; 2) support for AWS services - can the dev teams file tickets?...*
