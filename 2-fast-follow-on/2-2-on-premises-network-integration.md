# On-Premises Network Integration

This section addresses options and resources to enable network connectivity between your on-premises networks and AWS environment.

---
**Review Notes: For now add ideas and references to existing publicly available resources**

Let's build up ideas and refine as we go.

---

## Requirements

*...use the CAF perspectives to represent the typical set of customer requirements...*

*...list business use cases first along with outcomes...*

* Cloud client access to defined non-prod application and data services.
* On-premises access to newly deployed cloud hosted dev, test, prod workloads and services.
* Cloud client access to on-premises source code management access.
* Hybrid DNS resolution:
  * On-premises clients resolve custom FQDNs for cloud hosted services.
  * Cloud clients resolve customer FQDNs on on-premises services.
  
* Non-overlapping allocation of IP address ranges for use by cloud environments.

## Solution Options and Resources

*...typically start with site-to-site VPN based on speed of set up...*

*...defer to existing documentation including decision trees, blog posts, formal AWS docs, etc. as much as feasible...*

*...if the customer started with the use of temporary VPCs in support of their first few development environments, highlight considerations when migrating to the use of a set of new networks to support their development, test, and production environments...*
