# Solution Including Fast Follow-On Requirements

The following diagram highlights in green where and how the typical set of fast follow-on requirements can be met. If your organization’s needs dictate that some of these requirements must be satisfied from the start before formal development and testing can occur on AWS, you’ll need to allocate additional time for your initial build out.  The initial build out instructions in this guide refer to additional AWS guides to help you meet these requirements.

![alt text](https://github.com/ckamps/aws-foundation-journey/raw/master/images/dev-fast-follow-ons.png "Initial Development Environment with Fast Follow-On Capabilities")

Key aspects of a solution that supports the typical fast follow-on requirements include:

## Additional Development Team AWS Accounts

When your organization has more than one development team needing to use AWS, it’s straightforward to use AWS Control Tower and its built-in Account Factory product within AWS Service Catalog to provision a new standardized development AWS account for each new team.  AWS best practices recommend the use of separate team-based AWS accounts to avoid cloud resource conflicts between teams and to simplify cost reporting for this early stage in the lifecycle.

## Federated Access to AWS Platform Using Enterprise Standard Solution

Organizations typically integrate their existing enterprise standard SAML-based federated access solution with AWS so that coarse grained access control for AWS usage can be maintained via existing enterprise standard role and entitlement processes that are often based on Active Directory (AD) security group membership management. The AWS SSO service can be configured to integrate with standard SAML-based Identity Providers (IdPs) such as Okta, Azure AD, and Active Directory Federation Services (ADFS) to support this integration.

## On-Premises and AWS Cloud Network Integration

In many cases, organizations require that applications and workloads hosted in AWS can connect to workloads and shared services hosted on-premises and vice versa.  Typically, as an initial means to quickly establish this connectivity, one more VPN connections are established using existing on-premises network appliances and the AWS Site-to-Site VPN capability in conjunction with AWS Transit Gateway.  AWS Transit Gateway centralizes and simplifies sharing on-premises to AWS network integration across multiple VPCs.

In the solution diagram shown above, a new Network AWS account is shown as a means in which shared network resources such as the AWS Transit Gateway configuration can be isolated and managed separately from team oriented AWS accounts and the other shared accounts.

Longer term, as your on-premises to AWS network connectivity needs expand, you will typically transition from using site-to-site VPN connections to AWS Direct Connect.  When using AWS Transit Gateway as the termination point for VPN and AWS Direct Connect connections, a migration from using VPN to AWS Direct Connect has no impact on the VPCs behind the Transit Gateway.

If you didn’t use a non-overlapping range from the start, you will need to replace your initial set of development VPCs with VPCs that use non-overlapping IP addresses 

## Custom Security Guardrails and Foundation Baseline Resource Configurations

Once you move into a multi-AWS account architecture, your Cloud and Security Administrators will benefit from being able to centrally manage custom security guardrails and foundation baseline resource configurations that apply to your AWS accounts.

## Reuse of On-Premises Internet Ingress and Egress Security Services

In the initial solution, each development team’s account and VPC includes a series of public subnets, NAT Gateways, and direct access to the Internet via the AWS Internet Gateway capability.  Since your corporate intellectual property in the form of private source code will likely be present in your team development environments along with early forms of proprietary applications and services, your organization might not want to allow for direct access to the Internet from the development environments.

Under these circumstances, it is often most expedient to reuse your existing on-premises Internet security filtering capabilities to minimize the risk of IP and other information being leaked from your development environments to the Internet.   For example, as a tactical step, all egress traffic destined for the Internet from the cloud hosted development environments can be routed back on-premises over a site-to-site VPN connection and through existing network and security layers before being sent to the Internet.

Organizations often choose to disallow unsolicited inbound traffic from the Internet to their development networks to avoid the risk of development teams exposing IP and pre-production services to the Internet.

As part of introducing Internet security filtering for development environments, the public subnets, Internet Gateways, and NAT Gateways would be removed from each development VPC.

## Integration with Enterprise Security Information and Event Management (SIEM) Solution

Even in this early development stage, your Security and Compliance requirements may dictate that cloud platform access and cloud resource configuration be monitored via your existing enterprise standard Security Information and Event Management (SIEM) solution.
