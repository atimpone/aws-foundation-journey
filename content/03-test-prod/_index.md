---
title: 'Establish Test and Production Environments'
weight: 30
---

{{% notice note %}}
**Review Note:** The test and production envrionment section is only sketched out topically at this stage. We expect to begin addressing this section after drafting the higher priority [Fast Follow Capabilities]({{< relref "02-fast-follow" >}}) section. If you have comments and suggestions about this guide, see [Contributing]({{< relref "08-contributing" >}}).
{{% /notice %}}

Once you've establihed your initial foundation and delivered the initial set of development environments to teams, your next step is to extend your foundation by introducting a set of capabilities that organizations typically require before moving workloads into production.

[![Initial Test and Production Environments in Single AWS Region](/images/03-test-prod/test-prod-single-region.png)](/images/03-test-prod/test-prod-single-region.png)

## Refine Requirements and Identify Solutions

* Data Classification and Compliance
* Encryption
  * At Rest
  * In Transit
  * Key Management 
  * Certificate Management
* Multi-Region
* Test and Production AWS Account Design and Tenancy Model
  * Test, Production, and Builder Services AWS Accounts
  * Grouping like workloads together in same AWS accounts
* Test and Production Networks
  * VPC Design
  * On-premises Network Integration
  * DNS Integration
  * Internet Integration
* Initial Iteration of Workload Promotion and Release Management
* Evolved Foundation Baseline Management
* Cloud Operating Model
  * Defining who does what in terms of promotion and production operations
* Identity and Access Management
  * Enhanced Service Control Policies (SCPs)
  * IAM for:
    * Workloads
      * Runtimes
      * Lifecycle management
      * Operations and monitoring
    * Foundation
      * Runtimes
      * Lifecycle management
      * Operations and monitoring

## Build Out the Environments

* Build Test and Production AWS Accounts
* Establish Test and Product AWS Account Access Controls
* Enhance Development AWS Accounts with Production-like Access Controls (for early testing)
* Build Test and Production Networks
* Onboard Foundation Team
  * Promotion and Release Management
  * Operational Monitoring and Support
* Establish Encryption Support
* Establish Promotion and Release Management Process
* Onboard Development Teams
  * Ability to Perform Early Testing of Production-like Access Controls in Development
  * Promotion and Release Management
  * Operational Monitoring and Support
  
## Deploy Workloads and Operate the Environment

...