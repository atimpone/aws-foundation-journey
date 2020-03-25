# Structural

* DONE - Clean up page titles.
* DONE - Consider adjusting `#` to `##` to avoid conflict with page title.
* DONE - Incorporate dynamic TOCs to replace hardcoded TOCs.
* DONE - Correct internal links.
* DONE - Correct image references.
* DONE - Move notices to a more appropriate style.
* DONE - Make images linkable.
* DONE - List children on pages as appropriate.

Using anchors might not work:
```
Select the checkbox for each corresponding AWS SSO group based on [Mapping of Functional Roles to AWS SSO Groups]({{< relref "03-set-up-aws-platform-access-controls.md#2-map-foundation-functional-roles-to-existing-aws-groups" >}}).
```

# Learn Theme Mods

* Menu depth
https://github.com/matcornic/hugo-theme-learn/issues/88#issuecomment-437523806
https://github.com/matcornic/hugo-theme-learn/pull/195

# Content

* DONE - Change "Foundation Journey" to "Getting Started with AWS for First Formal Workloads"

* DONE - Change "developer team" to "builder team" throughout.
  * DONE - Add explanation of "builder" near front.

* DONE - Ensure landing/home page is appropriate.

* DONE - Add content to blank pages.

* DONE - Move future capabilities to new section at the end.

* DONE - Update README.md to:
  * Introduce the project.
  * Provide link to live web site.
  * Provide link to how to contribute.

# Look and Feel

* DONE - Reduce heading font sizes.
  * DONE - H3 needs to be smaller than H2.
* DONE - Make titles not be all caps.
* DONE - Disable copy to clipboard on `...` text fields.
* DONE - Incorporate settings from workshop: https://github.com/aws-samples/aws-modernization-workshop-sample
* DONE - AWS favicon

# Publish Draft and Obtain Feedback

* Push branch.
* Generate site and publish to S3 with CloudFront distro.
* Ask for feedback.

# Backlog / Nice to Have

* Reduce chapter headings in left menu font sizes.
* Inline TOCs
* Can children shortcode render ordered list? i.e. with numbers.
* Breadcrumbs
  * Long length of site title makes the breadcrumbs hard to use.
