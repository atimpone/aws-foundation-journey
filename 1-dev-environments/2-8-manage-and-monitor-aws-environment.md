# 8. Manage and Monitor Your AWS Environment

In this step your Cloud and Security Administrators and Cost Managers will review the typical day-to-day tasks and supporting services to help them manage and monitor your new AWS environment.

This step should take about 60 minutes to complete.

## Cloud Administrators

* Applying AWS Control Tower updates.
* Responding to alerts from AWS Control Tower guardrails and other AWS platform monitoring services.
* Monitoring costs across accounts on at least a weekly basis.

## Monitor and Manage Resource Configuration State

As resources are deployed in your account, managing the growing inventory of resources and ensuring that they are deployed consistently and maintained consistently can become a challenge. [AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html) is a Management and Governance tool available to help you with:

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

## Security Administrators

By following this guide, your foundation team has already established a foundation for security:

* Leveraged AWS Control Tower to set up and govern a secure, compliant, multi-account AWS environment based on best practices established by working with thousands of enterprises.
* Established mandatory [Guardrails](https://docs.aws.amazon.com/controltower/latest/userguide/guardrails.html) to provide ongoing governance for your overall AWS environment. Additional guardrails are available and should be reviewed by your security administrator and team.
* Established [AWS CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html) logging to capture all actions taken by users, roles and services across all of your AWS accounts.
* Secured the root user of your AWS accounts with multi-factor authentication (MFA).
* Set up an initial degree of AWS platform access management.

Beyond these capabilities that are already in place, you should plan on performing the following tasks: 

* Responding to alerts from AWS Control Tower guardrails and other AWS platform monitoring services.
* Onboarding and deprovisioning users and groups via AWS SSO.
* Modifying access permissions via AWS SSO Permission Sets.
* Performing periodic audits of your AWS security configuration.
    * Although some of the detective guardrails deployed through AWS Control Tower help continuously monitor and audit aspects of your AWS environment, it’s a best practice to periodically audit your security configuration to make sure that it meets your current business needs. See AWS [Security Audit Guidelines](https://docs.aws.amazon.com/general/latest/gr/aws-security-audit-guide.html) for best practices.


### 1. Review and Enable Foundational Security Services

While security is weaved within all AWS services and capabilities, a few explicit AWS Security, Identity, & Compliance services you should be aware of at this point in your journey are: 

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

### 2. Access CloudTrail

AWS CloudTrail is an AWS service that helps you enable governance, compliance, and operational and risk auditing of your AWS account. Actions taken by a user, role, or an AWS service are recorded as events in CloudTrail. Events include actions taken in the AWS Management Console, AWS Command Line Interface, and AWS SDKs and APIs.

1. Sign in to the AWS Management Console and open the CloudTrail console at https://console.aws.amazon.com/cloudtrail/home/.
2. Review the information in your dashboard about the most recent events that have occurred in your AWS account. One of these events should be a "ConsoleLogin" event, showing that you just signed in to the AWS Management Console.
3. Expand the event to see additional information.
4. As your usage of the platform grows you will find value in additional capabilities like search, filtering, and exporting the CloudTrail data.

### 3. Access CloudWatch

Amazon CloudWatch monitors your Amazon Web Services (AWS) resources and the applications you run on AWS in real time. You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and applications.
The CloudWatch home page automatically displays metrics about every AWS service you use. You can additionally create custom dashboards to display metrics about your custom applications, and display custom collections of metrics that you choose.

1. Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/
2. Notice that you can use the navigation bar to change the region to the region where you have your AWS resources. As you build out your environment, take note of the regions you use and be sure to leverage CloudWatch to monitor the resources in each.

At this stage without any workloads deployed, your CloudWatch data will be sparse. Once you are ready to configure monitoring, follow the [Getting Started with Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/GettingStarted.html) guidance.

### 4. Security Checklist Validation

Finally, once you have deployed resources in your account, a good checklist to review for security best practices can be found in the [AWS Security Checklist (PDF)](https://d1.awsstatic.com/whitepapers/Security/AWS_Security_Checklist.pdf). Become familiar with the checklist items and periodically review your account against its guidelines.

## Cost Managers

AWS Cost Management tools give you and your team visibility into AWS account costs and usage. Each account you create will have access to view their individual account costs and usage. The Master account can see the total organizational cost and usage rollup.

### 1. Access the Billing and Cost Management Dashboard

Sign in to the AWS Management Console and open the Billing and Cost Management console at [https://console.aws.amazon.com/billing/home#/](https://console.aws.amazon.com/billing/home)

There are a range of AWS Cost Management tools to help you access, organize, understand, control, and optimize your costs. You start to access detailed information about your AWS costs and usage using the built-in dashboard in the Billing and Management area of the AWS Management Console. 

### 2. Enable Cost Explorer

To see more detailed cost information for your account, you will want to enable the Cost Explorer:

1. Sign in to the AWS Management Console and open the Billing and Cost Management console at [https://console.aws.amazon.com/billing/home#/](https://console.aws.amazon.com/billing/home)
2. On the navigation pane, choose **Cost Explorer**. 
3. On the **Welcome to Cost Explorer** page, choose **Enable Cost Explorer**. 

### 3. Create a Budget

For more proactive management of your AWS costs, set up budgets within the Billing and Management console. Budgets allow you to:

* View your usage against a planned/budgeted amount.
* See where your usage is within free tier limits and limits you set.
* Estimate your usage each month based on consumption of the budget
* Make decisions on frequently updated usage and cost data. Budget data is updated three times each day to give you the most accurate information.
* Create alerts based on a budget to notify you or others as budget thresholds are reached. Each budget alert notification can be sent to up to 10 email addresses and 1 SNS topic for subscribers.

Take a few minutes and create an initial basic budget by following this guide [Create your first Budget](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/budgets-create.html).
   
## Next Steps

Review the other guides including Establishing Fast Follow-on Capabilities and Establishing Initial Test and Production Environments in the [main documentation](../README.md)
