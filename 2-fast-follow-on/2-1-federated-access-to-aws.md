# Federated Access to AWS Platform

This section addresses the typical requirements, solution options, and references to information to help you determine your direction to enable your internal users federated access to your AWS environment by using an identity proivider external to AWS. 

## Out of Scope: Application Level Federated Access

The section does not address federated access in support or your applications hosted on AWS. Although your enterprise identity and access management solution may also be used in support of application level federated access, different considerations and mechanisms come into play in this simialr, but different use case.

## Common Practices
It is common practice for organizations to reuse their existing enterpise identity and access management solution to form the basis of controlling access to the AWS platform.  Often, the source of truth for users and group-based entitlement definitions is based in Active Directory (AD) and often exposed via SAML-based Identity Providers (IdPs) for integration with publicly accessible services including SaaS services and cloud platforms such as AWS.

---
**Review Notes: For now add ideas and references to existing publicly available resources**

Let's build up ideas and refine as we go.

---

## Requirements

*...use the CAF perspectives to represent the typical set of customer requirements...*

## Solution Options and Resources

*...defer to existing documentation including decision trees, blog posts, formal AWS docs, etc. as much as feasible...*

*...if the customer started with the use of locally managed users and groups in AWS SSO, highlight considerations when miograting to the use of external identity providers either via AWS SSO or traditional federated access to AWS outside of AWS SSO...*
