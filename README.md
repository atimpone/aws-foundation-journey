# AWS Foundation Journey - Early Stages

Some Amazon Web Services (AWS) customers have expressed the need to have a perscriptive guide to help their organizations better understand how they can get started with the AWS platform when they are ready to move from the informal stage of using personal AWS accounts to the next stage of performing more formal collaborative experiments, initial development, and testing work that will likely result in an initial set of application and/or data services being deployed to production. 

The documents provided in this repository are part of an ongoing project to share AWS foundational architecture best practices which enable the quick deployment of secure environments in which teams can start collaborating on and experimenting with new ideas with the expectation that some of the results will need to move rapidly from development to test and production.

---
> ***The current focus of this project is to complete the first guide, "Establish Initial Development Environments". As the authors encounter best practices and resources associated with the subjects of the other guides outlined below, they will continue to add notes and links in those remaining guides.***
---
* [Stages of Cloud Adoption](#stages-of-cloud-adoption)
* [Cloud Foundation](#cloud-foundation)
* Guides
  * [Establish Initial Development Environments](#establish-initial-development-environments)
  * [Establish Fast Follow-On Capabilities](#establish-fast-follow-on-capabilities)
  * [Establish Initial Test and Production Environments](#establish-initial-test-and-production-environments)

## Stages of Cloud Adoption

Based on years of experience in helping customers obtain business benefits of cloud adoption, AWS has identified the following mental model to represent the [stages of cloud adoption](https://aws.amazon.com/blogs/enterprise-strategy/the-journey-toward-cloud-first-the-stages-of-adoption/).  

<img src="images/cloud-adoption-framework.png" alt="Cloud Adoption Framework" width="400"/>

Organizations leveraging these guides are typically in the “Project” phase of adoption during which they are starting with a few projects to begin to understand how they can leverage the cloud to meet a business need.

Once an enterprise has gained some benefit from the cloud by taking a few projects to production, an organization tends to move toward a "Foundation" phase in which the organization makes more extensive investments in its cloud foundation in support of scaling cloud adoption across the organization with the goal of gaining more extensive business benefits. 

Even in the initial project phase of adoption, AWS recommends that an initial cloud foundation be established that can be extended over time as organizations transition into the foundation phase to prepare for larger scale cloud adotpion. These guides help organizatins establish the beginning of their foundation on AWS in support of their initial few projects.

## Initial Form of Cloud Foundation

A key element of making the transition from the use of invididual user AWS accounts for early experiments to more formal initial work with the cloud is to ensure that your organization establishes a sufficiently secured and maintained initial form of your AWS cloud foundation.

In support of your first few formal projects, these guides start with getting an initial foundation and several development environments in place before address how to extend your foundation to support deploying your first few workloads to test and production environments. 

Later, when your organization has demonstrated success with the initial few projects, you will likely make a larger investment in your cloud foundation to support cloud adopton at scale.

<img src="images/foundation.png" alt="Cloud Foundation" width="700"/>

## Guides

### Establish Initial Development Environments

By following this guide, in as little as a few hours, your organization can establish an initial secure foundation and development environment in AWS.

#### Review and Refine Requirements and Solution Design

1. [Review and Refine Initial Development Environment Requirements](1-dev-environments/1-1-requirements.md)
2. [Review and Refine Initial Development Environment Solution](1-dev-environments/1-2-solution.md)

#### Build Out the Environment

1. [Map People to Foundation Functional Roles](1-dev-environments/2-1-map-people-to-foundation-roles.md)
2. [Create a New Master AWS Account](1-dev-environments/2-2-create-master-aws-account.md)
3. [Set Up an Initial Landing Zone Using AWS Control Tower](1-dev-environments/2-3-set-up-landing-zone.md)
4. [Set Up Initial AWS Platform Access Controls](1-dev-environments/2-4-set-up-aws-platform-access-controls.md)
5. [Create the Initial Team Development Environments](1-dev-environments/2-5-create-team-dev-environments.md)
6. [Establish Initial AWS Platform Monitoring Practices](1-dev-environments/2-6-initial-aws-platform-monitoring.md)
7. [Onboard the Initial Development Teams](1-dev-environments/2-7-onboard-dev-teams.md)
8. [Manage Your AWS Environment Going Forward](1-dev-environments/2-8-manage-aws-environment.md)

#### Reference

* [Cloud Platform System AWS Users](1-dev-environments/3-1-cloud-platform-system-users.md)

### Establish Fast Follow-On Capabilities

Depending on your organizations needs, some additional capabilities may be required either as part of your initial build out of development environments or shortly thereafter. This guide highlights the most common "fast follow-on" capabilities and provide references to current best practices to establish the capabilities.

#### Review and Refine Requirements and Solution Design

* [Review and Refine Initial Development Environment Fast Follow-On Requirements](2-fast-follow-on/1-1-requirements.md)
* [Review and Refine Initial Development Environment Fast Follow-On Solution](2-fast-follow-on/1-2-solution.md)

#### Build Out the Capabilities
---
> *The following sections have not yet been drafted. Initially, they will hold a series of notes and links to existing best practices and resources.*
---
* [Establish Federated Access to Your AWS Environment](2-fast-follow-on/2-1-federated-access-to-aws.md)
* [Set Up On-Premises Network Integration](2-fast-follow-on/2-2-on-premises-network-integration.md)
* [Enable Custom AWS Account Baselines](2-fast-follow-on/2-3-custom-account-baselines.md)
* [Establish Secure Internet Integration](2-fast-follow-on/2-4-secure-internet-integration.md)
* [Integrate with Security Information and Event Management (SIEM) Solution](2-fast-follow-on/2-5-siem-integration.md)

### Establish Initial Test and Production Environments
---
> *Other than the inclusion in the Solution Overview section of a rough diagram of a typical layout of the foundation including the addition of test and production environments, the sections for this guide have not yet been drafted. Initially, they will hold a series of notes and links to existing best practices and resources.*
---
The next guide that is under development helps you extend your foundation by introducting a set of capabilities organizations typically require before moving any workload into production.

#### Review and Refine Requirements and Solution Design

* [Review and Refine Initial Test and Production Environment Requirements](3-test-production/1-1-requirements.md)
* [Review and Refine Initial Test and Production Environment Solution](3-test-production/1-2-solution.md)

#### Build Out the Environments

* TBD
