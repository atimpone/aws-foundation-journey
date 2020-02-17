# Enhanced Security Monitoring and Compliance

This section addresses requirements, options, and resources to enable your Security and Cloud Administrators to extend the degree of preventative, detective, and corrective controls.

Support for [custom AWS account baselines](./2-3-custom-account-baselines.md) can be the means to roll out such controls, but this section focuses on what controls are of most interest.

## Examples

* An application requires a named IAM user to access the AWS platform with an API key and secret, configure additional alarms and logs when these credentials are used.
* Restricting the AWS regions in which your teams can deploy resources.
* Restricting the set of AWS services that are accessible to development teams.
* Expunge default VPCs from all AWS accounts and AWS regions in those accounts.
* Restrict access to AWS services to only the enterprise’s IP addresses.
