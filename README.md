# Get Started with AWS for Initial Formal Projects

---
***DRAFT CONTENT***

Content in this repository is in a preliminary draft form and should not be used for formal build outs of AWS environments unless an AWS specialist is working with you.  

The documentation is currently undergoing rapid changes as it is reviewed and tested.  

If you'd like to contribute via feedback, bug fixes, and/or enhanced content, see [CONTRIBUTING](CONTRIBUTING.md)

---

Some Amazon Web Services (AWS) customers have expressed the need to have a perscriptive guide to help their organizations better understand how they can get started with the AWS platform when they are ready to move from the informal stage of using personal AWS accounts to the next stage of performing more formal experiments, initial development, and testing work that will likely result in an initial set of application and/or data services being deployed to production. 

The documents provided in this repository are part of an ongoing project to share AWS foundational architecture best practices which enable the quick deployment of secure environments in which teams can start collaborating on and experimenting with new ideas with the expectation that some of the results will need to move rapidly from development to test and production.

---
**Review Note: Current focus is to complete the first guide: "Establish Initial Development Environments"**

As the authors encounter best practices and resources associated with the subjects of the other guides outlined below, they will continue to add notes and links in those remaining guides.

---

Background

* [Stages of Cloud Adoption](#stages-of-cloud-adoption)
* [Cloud Foundation](#initial-cloud-foundation-in-project-stage)
* [Project Tenets](0-common/1-tenets.md)
* [Frequently Asked Questions (FAQs)](0-common/2-faq.md)

Guides

1. [Establish Initial Development Environments](#1-establish-initial-development-environments)
2. [Establish Fast Follow-On Capabilities](#2-establish-fast-follow-on-capabilities)
3. [Establish Initial Test and Production Environments](#3-establish-initial-test-and-production-environments)

## Stages of Cloud Adoption

Based on years of experience in helping customers obtain business benefits of cloud adoption, AWS has identified the following mental model to represent the [stages of cloud adoption](https://aws.amazon.com/blogs/enterprise-strategy/the-journey-toward-cloud-first-the-stages-of-adoption/).  

<img src="images/cloud-adoption-framework.png" alt="Cloud Adoption Framework" width="400"/>

Organizations leveraging these guides are typically in the “Project” stage of adoption during which they are starting with a relatively small set of people and a few projects to begin to understand how they can leverage the cloud to meet a business need.

Once an enterprise has gained some benefit from the cloud by taking a few projects to production, an organization tends to move toward a "Foundation" stage in which the organization makes more extensive investments in boths its people and its cloud foundation in support of scaling cloud adoption across the organization with the goal of gaining more extensive business benefits. 

## Initial Cloud Foundation in Project Stage

Even in the initial project stage of adoption, AWS recommends that an initial foundation be established that can be extended over time as organizations transition into the foundation stage to prepare for larger scale cloud adoption. These guides help organizations establish the beginning of a secure foundation on AWS in support of their initial few projects.

In support of your first few formal projects, these guides start with establishing an initial foundation and several development environments before the guides address how to extend your foundation to support deploying your first few workloads to test and production environments. 

Later, after your organization has demonstrated success with the initial few projects, you will likely make larger investments during the foundation stage of your journey to support cloud adoption at scale.

<img src="images/foundation.png" alt="Cloud Foundation" width="700"/>

---

## 1. Establish Initial Development Environments

By following this guide, your organization can establish an initial secure foundation and development environments in AWS in less than a day.

![alt text](https://github.com/ckamps/aws-foundation-journey/raw/master/images/dev-initial.png "Initial Development Environment")

### Perform Up-front Tasks

1. [Review and Refine Initial Development Environment Requirements](1-dev-environments/1-1-requirements.md)
2. [Review and Refine Initial Development Environment Solution](1-dev-environments/1-2-solution.md)
3. [Map People to Foundation Functional Roles](1-dev-environments/1-3-map-people-to-foundation-roles.md)
4. [Address Pre-Requisites](1-dev-environments/1-4-address-pre-requisites.md)

### Build Out the Environment

1. [Create New Master AWS Account](1-dev-environments/2-1-create-master-aws-account.md)
2. [Set Up Initial Landing Zone Using AWS Control Tower](1-dev-environments/2-2-set-up-landing-zone.md)
3. [Set Up Initial AWS Platform Access Controls](1-dev-environments/2-3-set-up-aws-platform-access-controls.md)
4. [Onboard Foundation Team](1-dev-environments/2-4-onboard-foundation-team.md)
5. [Set Up Shared Development Network](1-dev-environments/2-5-set-up-shared-dev-network.md)
6. [Create Initial Team Development Environments](1-dev-environments/2-6-create-team-dev-environments.md)
7. [Onboard Development Teams](1-dev-environments/2-7-onboard-dev-teams.md)
8. [Manage and Monitor Your AWS Environment](1-dev-environments/2-8-manage-and-monitor-aws-environment.md)

### Reference

* [Getting Started Guide for Development Teams](1-dev-environments/3-1-getting-started-guide-dev-teams.md)
* [Cloud Platform System AWS Users](1-dev-environments/3-2-cloud-platform-system-users.md)
* [Sample IAM Policy for Developmemt Teams](1-dev-environments/3-3-iam-policy-infra-dev-team.md)

---

## 2. Establish Fast Follow-On Capabilities

Depending on your organizations needs, some additional capabilities may be required either as part of your initial build out of development environments or shortly thereafter. The following guides address the most common "fast follow-on" capabilities and provide references to current best practices to establish these capabilities.

![alt text](https://github.com/ckamps/aws-foundation-journey/raw/master/images/dev-fast-follow-ons.png "Initial Development Environment with Fast Follow-On Capabilities")

---
**Review Note: These sections have not yet been drafted**

Currently, they contain a series of notes and links to existing best practices and resources.  The following list will likely change to be ordered by priority.

---

Cost Management and Billing

* [Move to Invoice Billing](2-fast-follow-on/2-8-invoice-billing.md)

Security and Compliance

* [Establish Federated Access to Your AWS Environment](2-fast-follow-on/2-1-federated-access-to-aws.md)
* [Enable Secure Terminal Access to OS Instances](2-fast-follow-on/2-11-secure-terminal-access-to-os.md)
* [Enhance Access Controls](2-fast-follow-on/2-7-enhanced-access-controls.md)
* [Enhance Security Monitoring and Compliance](2-fast-follow-on/2-6-enhanced-security-monitoring-and-compliance.md)
* [Integrate Security Information and Event Management (SIEM) Solution](2-fast-follow-on/2-5-siem-integration.md)

Network Integration

* [Design and Set Up On-Premises Network Integration](2-fast-follow-on/2-2-on-premises-network-integration.md)
* [Establish Secure Internet Integration](2-fast-follow-on/2-4-secure-internet-integration.md)

Foundation Management

* [Begin Adopting Infrastructure as Code (IaC)](2-fast-follow-on/2-9-infrastructure-as-code.md)
* [Enable Custom AWS Account Baselines](2-fast-follow-on/2-3-custom-account-baselines.md)
* Bring Other AWS Accounts Into Your AWS Account Structure
---

## 3. Establish Initial Test and Production Environments

The next guide that is under development helps you extend your foundation by introducting a set of capabilities organizations typically require before moving any workload into production.

![alt text](https://github.com/ckamps/aws-foundation-journey/raw/master/images/test-prod-single-region.png "Initial Test and Production Environments in Single AWS Region")

---
**Review Note: These sections have not yet been drafted**

Initially, they will hold a series of notes and links to existing best practices and resources.

---

### Review and Refine Requirements and Solution Design

* [Review and Refine Initial Test and Production Environment Requirements](3-test-production/1-1-requirements.md)
* [Review and Refine Initial Test and Production Environment Solution](3-test-production/1-2-solution.md)

### Build Out the Environments

* TBD

## Contributing

1. See the issues in this GitHub repository for outstanding enhancements and bugs.
2. See [CONTRIBUTING.md](./CONTRIBUTING.md) for the contribution process.


