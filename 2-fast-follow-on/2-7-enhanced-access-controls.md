# Enhanced Access Controls

## Examples

### Inhibit Development Teams from Modifying Foundation Resources

Dev teams are starting out with `AWSPowerUser` permissions which is pretty broad. With the intiail permissions, team members could inadvertently modify foundation resources such as:

* AWS Control Tower CloudFormation stacks.
* VPC resources.
* Other forthcoming baseline resources.
