# Contributing

* [Providing Feedback](#providing-feedback)
* [Fixing Bugs and Making Enhancements](#fixing-bugs-and-making-enhancements)
* [Working with Content](#working-with-content)

## Providing Feedback

File issues in the GitHub repository when you either encounter bugs in the documentation or have suggestions for enhancements.  The maintainers will review issues periodically, tag them as either bug reports or enhancements, and provide comments.

## Fixing Bugs and Making Enhancements

Beyond filing issues, we welcome your bug fixes and enhacenments.

1. Either identify an existing issue or file a new issue representing the changes you intend to submit.
1. Fork the repository.
1. Make and test your changes locally.
1. Issue a Pull Request (PR) and include the issue number as `# <issue number>` so that a link to the issue is automatically included in the PR.
1. Respond to any comments in the PR.

## Working with Content

### Documentation Style

#### Defer to External Docs Where Feasible

When there's modular, to the point official documentation that can be linked to, we prefer that route vs duplicating lengthy instructions within these guides.  

However, when any of the following conditions apply, in the interest of providing a cohesive user experience, we don't hesitate to put instructions in line:
  * Steps are so few and simple that it's not worth directing the reader to another document.
  * Our instructions require context or specific data to be used that other generic guides don't include.
  * Instructions in other docs are not directly linkable. For example, linking to a large PDF document and asking the reader to find a section for specific instructions is a non-starter for any maintline steps in these guides.

### Working with draw.io Files

The `.png` drawings used in this repository are created in the following manner:

1. Open the `.drawio` file of interest using either the free online version or your internal instance the draw.io.
1. Select the tab of interst.
1. Select "Edit -> Select All"
1. Select "File -> Export As -> PNG..."
1. Select "Selection Only" and "Crop".
1. Select "Export"
1. Select "Download"

Copy the exported PNG file to the `images/` folder and rename it to suit your needs.

Since the file name and tab name are used to create the file names of exported images, you can minimize work required to export images by ensuring that the tab names represent what you'd like to use for the image names.  When renaming, you'll just need to remove the file name that is included by default in the export image file name.
