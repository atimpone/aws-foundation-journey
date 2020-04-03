# Structural

* DONE - Clean up page titles.
* DONE - Consider adjusting `#` to `##` to avoid conflict with page title.
* DONE - Incorporate dynamic TOCs to replace hardcoded TOCs.
* DONE - Correct internal links.
* DONE - Correct image references.
* DONE - Move notices to a more appropriate style.
* DONE - Make images linkable.
* DONE - List children on pages as appropriate.
* DONE - Selectively include inline TOC after intro paragraphs.
* IN PROGRESS - Understand how the `date` field in frontmatter is used by Hugo. 
  * Currently these dates are hardcoded.
  * How does Hugo or the Learn theme represent page modification dates?
  * Is the `date` field used?
  * Can the dates be auto generated based on Git metadata?

```
---
title: "Controlling Builder Team Access to Development Environments"
menuTitle: "Controlling Builder Team Access"
date: 2020-03-22T10:18:20-07:00
draft: false
weight: 20
---
```

# Learn Theme Mods

* DONE - Included in local CSSFigure out a clean means of getting the following menu depth fix into the mainstream static content build process:
  * https://github.com/matcornic/hugo-theme-learn/issues/88#issuecomment-437523806
  * https://github.com/matcornic/hugo-theme-learn/pull/195

# Content

* DONE - Change "Foundation Journey" to "Getting Started with AWS for First Formal Workloads"
* DONE - Change "developer team" to "builder team" throughout.
  * DONE - Add explanation of "builder" near front.
* DONE - Ensure landing/home page is appropriate.
* DONE - Add content to blank pages.
* DONE - Move future capabilities to new section at the end.
* DONE - Update README.md to:
  * DONE - Introduce the project.
  * Provide link to live web site.
  * DONE - Provide link to how to contribute.

# Look and Feel

* DONE - Reduce heading font sizes.
  * DONE - H3 needs to be smaller than H2.
* DONE - Make titles not be all caps.
* DONE - Disable copy to clipboard on `...` text fields.
* DONE - Incorporate settings from workshop: https://github.com/aws-samples/aws-modernization-workshop-sample
* DONE - AWS favicon

# Publish Draft and Obtain Feedback

* DONE - Push branch.
* DONE - Generate site and publish to S3 with CloudFront distro.
* Ask for feedback.

# Automation

* Develop IaC CloudFormation templates for:
  * Web site: S3 + CloudFront distribution
  * CD Pipeline
    * Detect changes to master branch.
    * Rebuild, deploy locally, sanity test
    * Publish to S3 and invalidate via CloudFront
    * Post deployment sanity test.
* Formal vanity FQDN
* Support branches other than master

Resources / Examples:

* https://github.com/aws-samples/aws-modernization-workshop-sample/tree/master/modules/webhosting
* https://github.com/aws-samples/aws-modernization-workshop-sample/blob/master/webspec.yml
* https://github.com/aws-samples/eks-workshop/blob/master/codebuild-deploy.sh

# Backlog / Nice to Have

* BUG - Debug using anchors with `relref` shortcode. 
  * For example, the following does not work.

```
Select the checkbox for each corresponding AWS SSO group based on [Mapping of Functional Roles to AWS SSO Groups]({{< relref "03-set-up-aws-platform-access-controls.md#2-map-foundation-functional-roles-to-existing-aws-groups" >}}).
```

* BUG - Get the link icons next to each section header so that people can easily copy links to anchors.
  * Odd behavior on the site given that the hover works on many, but not all pages.
```
https://discourse.gohugo.io/t/adding-anchor-next-to-headers/1726/14
```

* Reduce the size of the real estate used for the site logo and search box.
* TOCs
  * Enhance toc shortcode to use bullets or not. For pages that don't have numbered headings, we will typically want bullets.
* DONE - Breadcrumbs
  * Long length of site title makes the breadcrumbs hard to use.
