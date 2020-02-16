# Frequently Asked Questions (FAQs)

## AWS Account Design

### Why aren't Sandbox AWS accounts included in the initial build out?

Since the premise of the initial guide is to help customers quickly establish a formal development environment in which development, experimentation, and early testing of the first few application and/or data services can take place before they are rapidly moved through formal testing environments and into production, the traditional role of sandbox accounts in which the organization's intellectual propertly (IP) is not allowed does not yet apply to the customer.

In this very first and minimal stage of the build out, there are similarities between the initial development AWS accounts and typical sandbox AWS accounts, for example, the initial lack of on-premises network integration and failrly wide ranging access to AWS services, but the expectation is that most customers will either 1) require such gaps to be addressed at the outset and before development teams are onboarded, or 2) quickly address these gaps as fast follow-on requirements.

In these respects, the initiall provisioned developemnt team AWS accounts will quickly evolve to take on these additional properties. Rather than characterizing the initial development team AWS accounts as sandbox AWS accounts and needing to rename and reposition them later, the decision was made to position them as formal development team AWS accounts from the start.

Similar to other aspect of overall AWS account design, the guide intentionally avoids overloading customers with the fuller to be state too early in their adoption journey. Down the road and perhaps in the larger "foundation" stage of adoption or earlier as a parallel workstream, the capability to provide true sandbox AWS accounts may be addressed depending on the customer needs.

## Federated Access to AWS Platform

### Why isn't federated access addressed from the start?

It is our belief that it might take 1-2 or more weeks for an organization to go through the necessary preparation and execution to get true federated access into place. The minimal form of the foundation uses locally managed groups and users in AWS SSO for the first few weeks until a more desirable federated access capability is established.