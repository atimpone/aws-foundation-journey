# 1. Map People to Foundation Roles

In this step you will identify the people who will play an initial set of roles in establishing, securing, and maintaining the cloud foundation so that your expectations are set in terms of accountability, ownership, and required skills and training.

This step should take about 30 minutes to complete subject to the proper stakeholders being involved in the meeting. 

The following table lists a typical set of minimal roles to own and manage your initial iteration of your cloud foundation. You should be able to identify 1-2 people in your organization who will plays these roles and have these responsibilities for at least this stage of your cloud adoption journey.

|Role	|Description	|Responsibilities	|
|---	|---	|---	|
|Cloud Administration	|Write access to cloud foundation resources.	|* Create and manage shared cloud infrastructure. For example:
    * AWS accounts
    * Shared networking resources.
* Onboard new development teams on usage of their cloud development environments.	|
|Security Administration	|Write access to cloud foundation security resources.	|* Create and manage baseline security policies in AWS.
* Monitor and respond to AWS usage security events.
* Learn and promote cloud security best practices.	|
|Cost Management	|Write access to cost budgets and reporting.	|* Monitor overall clound spend.
* Create, manage, and ensure access to cost and budget reports.
* Learn and apply fundamentals of cloud cost optimization practices.	|
|Audit	|Read only access to all AWS resources.	|Periodically review data hosted in AWS for compliance.	|
|	|	|	|
|	|	|	|

## Start With a Small Foundation Team

Typically, several capable infrastructure oriented engineers are identified to play the role of the initial set of cloud administrators. Playing this role effectively requires that it is treated as a full-time assignment.

In some cases, where the people resources can be made available and there’s a business need in this early stage, one to two people from your Security team may take on the role of Security Administration from the start.  In other cases, in this early stage, that role may be delegated to the same people who are playing the role of Cloud Administration.

Even in cases where roles are initially played by the same people, it’s recommended that you start with a separate set of technical roles so that, in the spirit of separation of duties, the access permissions are separated from the start and pave the way for an easier transition to a broader set of administrative teams as your adoption of the cloud expands.

A common mistake made in this early stage of the journey is to assume that people playing certain roles in your existing on-premises environment must play a set of corresponding roles in the cloud.  Although eventually many of your infrastructure and security people may transition to roles in managing your use of cloud resources, to start, it’s a best practice to have a small number of closely knit technical people manage your initial adoption of the cloud.

## Define Additional Foundation Roles Over Time

When adoption of the cloud expands and the foundation becomes more capable and complicated, you may chose to introduce additional foundation roles to spread the ownership and work of managing the foundation across more teams. For example, a Network Administration role played by Network Engineering team members may be useful as the cloud foundation networking capabilities expand over time. Another common example is for your Security Incident Response team to become more directly involved in the cloud and have a corresponding Incident Response role with appropriate access privileges.

## Use Distinct But Similar Development Team Roles

In addition to the foundation roles listed above, your initial build out of the foundation will include a set of roles to be used by teams that need to experiment, develop, and test early forms of business applications, data services, and foundation capabilities. In this sense, all of your technologists up and down the stack should be viewed as developers in their own right.

In order for your foundation engineers, data engineers, and application developers to be able to get things done in the cloud, you will be establishing a set of development team roles that provide these teams similar degrees of access, but in distinct, team-specific development AWS accounts.