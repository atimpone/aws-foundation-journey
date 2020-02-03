# Fast Follow-On Requirements

Depending on your organizations needs, you may need some of the following requirements addressed in the build out of your initial foundation and development environment.  Although addressing these requirements will add time to the overall initial build out, AWS provides additional guides and best practices to help you quickly meet those requirements. References to these additional guides are included in the build out steps later in this guide.

***Add table of contents***

## Development Team Requirements

* Integration with and connectivity to defined on-premises applications, data, and shared infrastructure services. For example:
    * Cloud client access to defined  non-prod application and data services.
    * On-premises source code management access.
    * Hybrid DNS resolution.
* Onboarding of additional teams with their own isolated development environments.

## Foundation Requirements

Broken down by the perspectives defined in the[AWS Cloud Adoption Framework](https://aws.amazon.com/professional-services/CAF/):

### Business

# Business
* Transition from credit card to invoice based billing and payment for AWS services.

# People
* Begin longer terms learning paths for Infrastructure as Code techniques.

### Technical

# Platform
* See the development team requirements listed above.

# Security
* Enable custom security guardrails across multiple AWS accounts.
* Constrain which AWS services can be accessed in development environments.
* Constrain which AWS regions can be used in development environments.
* Integrate existing centrally managed identity management services to control access to the AWS platform.
* Implement enterprise security inspection and filtering of ingress and egress access with the Internet.
* Restrict access to AWS services to only the enterprise’s IP addresses.
* Integrate enterprise Security Information and Event Management (SIEM) services.
    * AWS API usage (e.g. AWS CloudTrail logs)
    * AWS Resource Configuration changes (e.g. AWS Config)
    * Network traffic monitoring (e.g. partly based on capture of VPC Flow Logs)

# Operations
* Enable centralized management and distribution of foundation baseline configurations across AWS accounts.
* Establish network integration between on-premises and AWS:
    * Secure private network connectivity between on-premises and AWS to support initial on-premises and  AWS integration scenarios. 
    * Non-overlapping allocation of IP address ranges for use by development environments.