# Enhanced Access Controls

This section addresses requirements, options, and resources to enable your Security and Cloud Administrators to achieve further degrees of least privilege access to improve the security of the overall environments and stability of the foundation. 

## Examples

### Inhibit Development Teams from Modifying Foundation Resources

Teams using development AWS accounts are starting out with `AWSPowerUser` permissions which is pretty broad. With the intiail permissions, team members could inadvertently modify foundation resources such as:

* AWS Control Tower CloudFormation stacks.
* VPC resources.
* Other forthcoming baseline resources.
