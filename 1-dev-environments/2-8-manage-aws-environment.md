# 8. Manage Your AWS Environment Going Forward

Your Cloud Administrators and Security Administrators should be have the time and skills to perform the following tasks on an ongoing basis to support use of your AWS environment.

Cloud Administrators

* Applying AWS Control Tower updates.
* Responding to alerts from AWS Control Tower guardrails and other AWS platform monitoring services.
* Monitoring costs across accounts on at least a weekly basis.

Security Administrators

* Responding to alerts from AWS Control Tower guardrails and other AWS platform monitoring services.
* Onboarding and deprovisioning users and groups via AWS SSO.
* Modifying access permissions via AWS SSO Permission Sets.
* Performing periodic audits of your AWS security configuration.
    * Although some of the detective guardrails deployed through AWS Control Tower help continuously monitor and audit aspects of your AWS environment, it’s a best practice to periodically audit your security configuration to make sure that it meets your current business needs. See AWS [Security Audit Guidelines](https://docs.aws.amazon.com/general/latest/gr/aws-security-audit-guide.html) for best practices.
    
## Next Steps

Review the other guides including Establishing Fast Follow-on Capabilities and Establishing Initial Test and Production Environments in the [main documentation](../README.md)
