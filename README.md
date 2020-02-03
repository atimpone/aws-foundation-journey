# AWS Foundation Journey - Early Stages

***Does your organization need to quickly access a secure environment in which teams can start collaborating on and experimenting with new ideas with the expectation that some of the results will need to move rapidly from development to test and production?***

This repository contains a set of guides to help organizations better understand how they can get started with the Amazon Web Services (AWS) platform when they are ready to move from the informal stage of using personal AWS accounts to the next stage of performing more formal collaborative experiments, initial development, and testing work that will likely result in an initial set of application and/or data services being deployed to production. 

* [Purpose of These Guides](#purpose-of-these-guides)
* [Stages of Cloud Adoption](#stages-of-cloud-adoption)
* [Cloud Foundation](#cloud-foundation)
* Guides
  * [Establish Initial Development Environments](#establish-initial-development-environments)
  * [Establish Fast Follow-On Capabilities](#establish-fast-follow-on-capabilities)
  * [Establish Initial Test and Production Environments](#establish-initial-test-and-production-environments)

## Purpose of These Guides

The authors of these guides work with organizations who are new to the AWS platform and need guidance on getting started with their formal work with the platform using up-to-date best practices, AWS services, and features. 

Although there are many resources available to help organizations understand particular facets of this stage of the cloud adoption journey, the authors found that there was little im the way of prescriptive steps that help organiztions quickly get started with their formal build outs in AWS.

These guides strive to avoid duplicating existing AWS documentation and other resources by deferring to existing AWS documentation and other resources for much of the background and detailed information. 

Over time, these guides could potentially become incorpotated into formal AWS documentation.

## Stages of Cloud Adoption

Based on years of experience in helping customers obtain business benefits of cloud adoption, AWS has identified the following mental model to represent the [stages of cloud adoption](https://aws.amazon.com/blogs/enterprise-strategy/the-journey-toward-cloud-first-the-stages-of-adoption/).  

<img src="images/cloud-adoption-framework.png" alt="Cloud Adoption Framework" width="400"/>

Organizations leveraging these guides are typically in the “Project” phase of adoption during which they are starting with a few projects to begin to understand how they can leverage the cloud to meet a business need. 

Once an enterprise has gained some benefit from the cloud by taking a few projects to production, an organization tends to move toward a "Foundation" phase in which the organization makes more extensive investments in its cloud foundation in support of scaling cloud adoption across the organization while gaining more extensive business benefits. 

## Cloud Foundation

A key element of making the transition from the use of invididual user AWS accounts for early experiments to more formal initial work with the cloud is to ensure that your organization establishes a sufficiently secured and maintained initial form of your AWS cloud foundation.

In support of your first few formal projects, these guides start with getting an initial foundation and several development environments in place before address how to extend your foundation to support deploying your first few workloads to test and production environments. 

Since requirements vary across organizations, a series of supplemental guides address optional capabilities that often provide value even in this early stage of cloud adoption.

<img src="images/foundation.png" alt="Cloud Foundation" width="700"/>

## Guides

### Establish Initial Development Environments

By following this guide, in as little as a few hours, your organization can establish an initial secure foundation and development environment in AWS.

* [Initial Development Environment Requirements](1-dev-environments/1-1-requirements.md)
* [Initial Development Environment Solution Overview](1-dev-environments/1-2-solution.md)
* Build Out Steps
  1. [Map People to Foundation Roles](1-dev-environments/2-1-map-people-to-foundation-roles.md)
  2. [Create a New Master AWS Account](1-dev-environments/2-2-create-master-aws-account.md)
  3. [Set Up an Initial Landing Zone Using AWS Control Tower](1-dev-environments/2-3-set-up-landing-zone.md)
  4. [Set Up Initial AWS Platform Access Controls](1-dev-environments/2-4-set-up-aws-platform-access-controls.md)
  5. [Create the Initial Team Development Environments](1-dev-environments/2-5-create-team-dev-environments.md)
  6. [Establish Initial AWS Platform Monitoring Practices](1-dev-environments/2-6-initial-aws-platform-monitoring.md)
  7. [Onboard the Initial Development Teams](1-dev-environments/2-7-onboard-dev-teams.md)
  8. [Manage Your AWS Environment Going Forward](1-dev-environments/2-8-manage-aws-environment.md)
* Reference
  * [Cloud Platform System AWS Users](1-dev-environments/3-1-cloud-platform-system-users.md)


### Establish Fast Follow-On Capabilities

Depending on your organizations needs, the following capabilities may be required relatively early in your cloud adoption journey.

Initially, the following sections will contain rough notes on current best practices and links to existing resources.

* [Initial Development Environment Fast Follow-On Requirements](2-fast-follow-on/1-1-requirements.md)
* [Initial Development Environment Fast Follow-On Solution Overview](2-fast-follow-on/1-2-solution.md)
* Capabilities
  * [Federated Access to Your AWS Environment](2-fast-follow-on/2-1-federated-access-to-aws.md)
  * [On-Premises Network Integration](2-fast-follow-on/2-2-on-premises-network-integration.md)
  * [Custom AWS Account Baselines](2-fast-follow-on/2-3-custom-account-baselines.md)
  * [Secure Internet Integration](2-fast-follow-on/2-4-secure-internet-integration.md)
  * [Security Information and Event Management (SIEM) Integration](2-fast-follow-on/2-5-siem-integration.md)

### Establish Initial Test and Production Environments

The next guide that is under development helps you extend your foundation by introducting a set of capabilities organizations typically require before moving any workload into production.

* [Initial Test and Production Environment Requirements](3-test-production/1-1-requirements.md)
* [Initial Test and Production Environment Solution Overview](3-test-production/1-2-solution.md)
* Build Out Steps
  * TBD
