---
title: "Secure Internet Integration"
weight: 20
---

This section addresses options and resources to enable you to further secure Internet integration in support of your initial development environments and in preparation for establishing test and production hosting environments on AWS.

{{% notice note %}}
**Review Note: For now add ideas and references to existing publicly available resources:** Let's build up ideas and refine as we go.
{{% /notice %}}

## Requirements

In the initial stage of your foundation, you may have enabled development team AWS accounts direct bidirectional access to the Internet via use of public subnets, an AWS Internet Gateway, and AWS NAT Gateways.  Organizations that desire to avoid exposing development workloads and users directly to the Internet would rather funnel Internet ingress and egress traffic through centrally controlled proxies and security services.

Similar interests may come into play in support of workloads deployed to test and production hosting environments.

In the initial solution, each development team’s account and VPC includes a series of public subnets, NAT Gateways, and direct access to the Internet via the AWS Internet Gateway capability.  Since your corporate intellectual property in the form of private source code will likely be present in your team development environments along with early forms of proprietary applications and services, your organization might not want to allow for direct access to the Internet from the development environments.

## Solution Options and Resources

### Tactical Routing of Ingress and Egress Traffic Through Existing On-Premises Security Services
Under these circumstances, it is often most expedient to reuse your existing on-premises Internet security filtering capabilities to minimize the risk of IP and other information being leaked from your development environments to the Internet.   For example, as a tactical step, all egress traffic destined for the Internet from the cloud hosted development environments can be routed back on-premises over a site-to-site VPN connection and through existing network and security layers before being sent to the Internet.

The primary downsides of this tactical approach are:
* Increased in latency.
* Increased dependency on on-premises infrastructure.

### Longer Term Cloud Hosted Ingress and Egress Security Services

See [Nick Matthews' re:Invent 2019 talk](https://youtu.be/9Nikqn_02Oc?t=2304) on the role that AWS Transit Gateway can play in this regard.

### Impact to Development VPC Design

Organizations often choose to disallow unsolicited inbound traffic from the Internet to their development networks to avoid the risk of development teams exposing intellectual property (IP) and pre-production services to the Internet.

As part of introducing Internet security filtering for development environments, the public subnets, Internet Gateways, and NAT Gateways would be removed from each development VPC.