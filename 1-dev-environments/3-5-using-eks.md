# Using Amazon EKS in Your Development Environment

## Using `eksctl` CLI to Create a Cluster

* [Deploy and configure Cloud9 environment](3-2-getting-started-guide-dev-team-members.md#using-aws-cloud9-web-ide)
* Install `eksctl` and `kubectl` per [Getting Started with eksctl](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html).
  * Ensure that you have at least `eksctl` version `0.14.0` so that permissions boundary support is available.
* Review the set of public and private subnets in the **`VPC`** service within the AWS Management Console.

To Do:
* Factor in the use of the permissions boundary.
  
  ```
  eksctl create cluster --region us-east-2 --name nikki-dev \
      --vpc-private-subnets=subnet-...,subnet-...,subnet-... \
      --vpc-public-subnets=subnet-...,subnet-...,subnet-...
  ```
