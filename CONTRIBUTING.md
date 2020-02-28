# Contributing

* [Providing Feedback](#providing-feedback)
* [Fixing Bugs and Making Enhancements](#fixing-bugs-and-making-enhancements)
* [Working with Content](#working-with-content)

## Review the Work in Progress and Backlog

See the project [Kanban board](https://github.com/ckamps/aws-foundation-journey/projects/1?fullscreen=true) for the set of already files issues and work in progress.

## Providing Feedback

Either comment on existing issues or file new issues in the GitHub repository when you either encounter bugs in the documentation or have suggestions for enhancements.  The maintainers will review issues periodically, tag them as either bug reports or enhancements, and provide comments.

## Fixing Bugs and Making Enhancements

Beyond filing issues, we welcome your bug fixes and enhacenments.

1. Either identify an existing issue or file a new issue representing the changes you intend to submit.
1. Fork the repository.
1. Make and test your changes locally.
1. Issue a Pull Request (PR) and include the issue number as `# <issue number>` so that a link to the issue is automatically included in the PR.
1. Respond to any comments in the PR.

## Working with Content

### Defer to External Docs Where Feasible

When there's modular, to-the-point official documentation that can be linked to, we prefer that route vs duplicating lengthy instructions within these guides.  

However, when any of the following conditions apply, in the interest of providing a cohesive user experience, we don't hesitate to embed instructions inline:
  * Steps are so few and simple that it's not worth distracting the reader by forcing them to go to another document.
  * The instructions require context or specific data to be used that other more general purpose guides don't include.
  * Instructions in other docs cannot be directly accessed via a link. For example, linking to a large PDF document and asking the reader to find a section for specific instructions is a non-starter in terms of the user experience.

### Working with draw.io Files

The `.png` drawings used in this repository are created in the following manner:

1. Open the `.drawio` file of interest using either the free online version or your internal instance of draw.io.
1. Select the tab of interst.
1. Select "Edit -> Select All"
1. Select "File -> Export As -> PNG..."
1. Select "Selection Only" and "Crop".
1. Select "Export"
1. Select "Download"

Copy the exported PNG file to the `images/` folder and rename it to suit your needs.

#### Tab Names in drawio Files

Since the file name and tab name are used to create the file names of exported images, you can minimize work required to export images by ensuring that the tab names represent what you'd like to use for the image names.  When renaming, you'll just need to remove the file name that is included by default in the export image file name.

### Linking to Images

#### Relative Linking

Normally, when an image is easy to read inline, we use relative links:

```
<img src="images/cloud-adoption-framework.png" alt="Cloud Adoption Framework" width="400"/>
```

The downside of this approach is that clicking on the image does not immediately expand it. See the following approach when direct, immediate expansion is important.

#### Fully Qualified Linking

Although not preferred due to the awkwardness of testing changes in your local repositories, sometimes when the image is too hard to see inline, readers will benefit from being to click on the image to immediately explode it.

The least worst approach we've found is the following:

```
![alt text](https://github.com/ckamps/aws-foundation-journey/raw/master/images/dev-network-initial-details.png "Initial Network Details")
```

