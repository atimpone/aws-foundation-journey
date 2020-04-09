---
title: 'History of Changes'
menuTitle: 'Changes'
disableToc: true
weight: 50
---

A history of notable changes to the guide.

|Date|Change|Description|
|----|------|-----------|
|March 31 2020|**No longer share public subnets**|Share only private subnets with team development accounts so that builder teams can't enable Internet access to their development workloads.|
|March 27 2020|**Enhance team dev IAM policies with NotAction**|Using the AWS managed IAM policy PowerUser as a basis, make the SAML policy and permissions boundary more secure by default by patterning a portion of them after the PowerUser managed policy.|
|March 15 2020|**Convert to Hugo static site generator**|Make it easier to browse the guide via a web site as compared to browsing markdown files in the git repository.|
|March 1 2020|**Initial form of team dev access controls based on IAM permissions boundaries**|A means to enable builder teams with wide ranging access, but not able to modify the underlying foundation resources.|
