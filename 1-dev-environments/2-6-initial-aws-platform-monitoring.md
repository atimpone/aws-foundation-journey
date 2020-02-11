# 6. Establish Initial AWS Platform Monitoring Practices

*Think about what the cloud admins, security, and finance teams will be most concerned with in terms of monitoring the overall environment. For example:*

* *Cost*
* *Security*
    * *AWS Control Tower Guardrails*
        * *Are there any optional guardrails that should be enabled at this time?*
    * *Amazon GuardDuty*
* *Overall AWS Environment Monitoring*
    * *AWS Trusted Advisor is a good example.*

*In support of each of the perspectives above: *

* *Introduce a capability and supporting AWS service that is useful and easy to enable at this stage.*
    * *Highlight what the capability is and the value it provides.*
* *Highlight what has to be done to enable the capability if it’s not already enabled. *
    * *Link to existing docs for details.*
* *Highlight the typical for enabling the capability given several development accounts + core accounts and a typical set of development and testing activities across the two dev accounts.*
* *Highlight how the capability can be leveraged on an ongoing basis.*
    * *For example:*
        * *Will alerts or reports be automatically sent to email addresses/distribution lists?*
        * *Does it entail periodic review?*
    * *Link to existing docs for detailed set up instructions.*

* * *
In this step your Cloud Admins, Security Admins, and Cost Managers will become familiar with the basic monitoring and management capabilities for your new AWS environment including:

* Costs
* Security
* Resource configuration state

 
This step should take about 60 minutes to complete.

### Monitor and Manage Costs

AWS Cost Management tools give you and your team visibility into AWS account costs and usage. Each account you create will have access to view their individual account costs and useage. The Master account can see the total organizatonal cost and usage rollup.

## 1. Access the Billing and Cost Management Dashboard

1. Sign in to the AWS Management Console and open the Billing and Cost Management console at [https://console.aws.amazon.com/billing/home#/](https://console.aws.amazon.com/billing/home)
2. 

There are a range of AWS Cost Management tools to help you access, organize, understand, control, and optimize your costs. You start to access detailed information about your AWS costs and usage using the built-in dashboard in the Billing and Management area of the AWS Management Console. 

## 2. Enable Cost Explorer

To see more detailed cost information for your account, you will want to enable the Cost Explorer:

1. Sign in to the AWS Management Console and open the Billing and Cost Management console at [https://console.aws.amazon.com/billing/home#/](https://console.aws.amazon.com/billing/home)
2. On the navigation pane, choose **Cost Explorer**. 
3. On the **Welcome to Cost Explorer** page, choose **Enable Cost Explorer**. 

## 3. Create a Budget

For more proactive management of your AWS costs, consider setting up budgets within the Billing and Management console. Budgets allow you to:

* View your usage against a planned/budgeted amount.
* See where your usage is within free tier limits and limits you set.
* Estimate your usage each month based on consumption of the budget
* Make decisions on frequently updated usage and cost data. Budget data is updated three times each day to give you the most accurate information.
* Create alerts based on a budget to notify you or others as budget thresholds are reached.

Take a few minutes and create an initial basic budget by following this guide [Create your first Budget](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/budgets-create.html).



### Monitor and Manage Security

At this point in your journey to establish your first secure AWS development environment we have already established an excellent foundation for security. We have:

* Leveraged AWS Control Tower to set up and govern a secure, compliant, multi-account AWS environment based on best practices established by working with thousands of enterprises.
* Established mandatory [Guardrails](https://docs.aws.amazon.com/controltower/latest/userguide/guardrails.html) to provide ongoing governance for your overall AWS environment. Many more recommended guardrails are available and should be reviewed by your security administrator and team.
* Established **[AWS CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html) **logging to capture all actions taken by users, roles and services within your AWS accounts.
* Secured your root account with multi-factor authentication (MFA)
* Setup basic AWS platform access management

 
While security is weaved within all AWS services and capabilities, a few explicit AWS Security, Identity, & Compliance services you should be aware of at this point in your journey are: 
**** ****
****[Amazon GuardDuty](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)**** is our threat detection service that continuously monitors for malicious activity and unauthorized behavior to protect your AWS accounts and workloads. To use GuardDuty, it is a service that needs to be enabled. We recommend [enabling](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_settingup.html) the service for the 30-day free trial and see the visibility and value it brings to your security practice.

****[AWS Shield](https://docs.aws.amazon.com/waf/latest/developerguide/shield-chapter.html)**** is a managed Distributed Denial of Service (DDoS) protection service that safeguards applications running on AWS. AWS Shield provides always-on detection and automatic inline mitigations that minimize application downtime and latency, so there is no need to engage AWS Support to benefit from DDoS protection. There are two tiers of AWS Shield - Standard and Advanced. All AWS customers benefit from the automatic protections of AWS Shield Standard, at no additional charge.

****[AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/)**** is an online tool that provides you real time guidance to help you provision your resources following AWS best practices. You will get access to the seven core Trusted Advisor checks to help increase the security and performance of your AWS environment including:

* ****Security****
    * S3 Bucket Permissions
    * Security Groups - Specific Ports Unrestricted
    * IAM Use
    * MFA on Root Account
    * EBS Public Snapshots
    * RDS Public Snapshots
* ****Service Limits****


Finally, once you have deployed resources in your account, a good checklist to review for security best practices can be found in the [AWS Security Checklist (PDF)](https://d1.awsstatic.com/whitepapers/Security/AWS_Security_Checklist.pdf).
 

### Monitor and Manage Resource Configuration State

As resources are deployed in your account, managing the growing inventory of resources and ensuring that they are deployed consistently and maintained consistently can become a challenge. **[AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html)** is a Management and Governance tool available to help you with:

* Resource Administration and Governance
* Auditing and Compliance
* Managing and Troubleshooting Configuration changes
* Security Analysis

More specifically, you can do the following with AWS Config:

* Evaluate your AWS resource configurations for desired settings.
* Get a snapshot of the current configurations of the supported resources that are associated with your AWS account. 
* Retrieve configurations of one or more resources that exist in your account.
* Retrieve historical configurations of one or more resources.
* Receive a notification whenever a resource is created, modified, or deleted.
* View relationships between resources. For example, you might want to find all resources that use a particular security group. 

Once you have resources deployed in your account, consider [Getting Started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html).

## Next Steps

[7. Onboard the Initial Development Teams](2-7-onboard-dev-teams.md)
