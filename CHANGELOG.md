# History of Significant Changes


## Guide: Establish Initial Foundation and Development Environemnts

February 28, 2020

### Draft Form of Permissions Boundary to Inhibit Privilege Escalation in Development AWS Accounts

A draft form of AWS IAM Permissions Boundary support was incorporated in the guide to fill a privilege escalation gap in the development team permissions approach. 

As noted in previous drafts, the initial form of the development team permissions did not inhibit developers from creating IAM roles that could circumvent the desired goals of the development team permissions. 

With the advent of the draft form of a permissions boundary, further controls are put in place to fill the escalation gap.

If you already built out your initial development environment and would like to experiment with the draft permissions boundary:

1. Review [Controlling Development Team Access](1-dev-environments/3-3-controlling-dev-team-access.md).
2. Follow the new step [Distribute Permissions Boundary to Development OU](1-dev-environments/2-3-set-up-aws-platform-access-controls.md#8-distribute-permissions-boundary-to-development-ou) in section [3. Set Up Initial AWS Platform Access Controls](1-dev-environments/2-3-set-up-aws-platform-access-controls.md).
3. Along the lines of step [Create Development Team Permission Set in AWS SSO](1-dev-environments/2-3-set-up-aws-platform-access-controls.md#8-create-development-team-permission-set-in-aws-sso):
    1. Edit the existing permission set in AWS SSO and replace the policy with the latest form of the sample policy.
    2. Deploy the updated policy to all of the development AWS accounts.
4. See the bottom of [Controlling Development Team Access](1-dev-environments/3-3-controlling-dev-team-access.md) for test scenarios that you can try out.
