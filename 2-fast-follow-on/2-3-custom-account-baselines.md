# Custom AWS Account Baselines

This section reviews the typical requirements, introduces common solution options, and provides references to further information to help you determine your approach and enable your foundation team to define and efficiently roll out new and updated cloud resources or "baselines" across your AWS accounts to further secure the overall environment and deliver useful common capabilities to your internal teams. 

## Examples

For example, you will likely gain value from:

* Restricting the AWS regions in which your teams can deploy resources.
* Reducing the set of AWS services that development teams can use in their development AWS accounts so that access to services that are likely not important to your business are disallowed.
* Refining the degree of access development teams have in their development AWS accounts. For example, you likely don't want development team members to be able to modify stable foundation team managed resources residing in the development team AWS accounts.

These are just several examples of many that are common for organizations starting out with AWS.

## Automation and Infrastructure as Code (IaC)

As the degree of customization and extent of your foundation resources expands over time, you'll benefit for having an automated means to roll out and manage such resources.  Additionally, you'll benefit from using Infrastructure as Code (IaC) and other common practices to treat such resources as code that progresses through a modern development and testing worklow.

---
**Review Notes: For now add ideas and references to existing publicly available resources**

Let's build up ideas and refine as we go.

---

## Requirements

*...use the CAF perspectives to represent the typical set of customer requirements...*

## Solution Options and Resources

*...highlight that AWS Control Tower is addressing many commonly needed security related baseline configurations via "guardrails", but does not yet have the capability to support customer security guardrails and more general foundation resource configurations...*

*...Note the ability of AWS CloudFormation StackSets to be applied at the OU level and automatically re-applied as the membership of a given OU changes...*

*...defer to existing documentation including decision trees, blog posts, formal AWS docs, etc. as much as feasible...*
