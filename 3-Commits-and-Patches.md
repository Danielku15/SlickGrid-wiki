# Commit and patch list

To this end, I'm providing each GIT patch for download, plus maintaining the [6pac/SlickGrid](https://github.com/6pac/SlickGrid) master repo 
as a fork of mleibman/SlickGrid master with all the patches applied. Thus 6pac/SlickGrid should be an up-to-date, ready-to-download version 
of the latest SlickGrid master. Or, you can apply the individual patches to your own repo. Your choice.

The master repo: [6pac/SlickGrid](https://github.com/6pac/SlickGrid)

Essential Patches
-----------------

These patches are for bugs or known issues with mleibman/SlickGrid master

<a href="01-lib-patch.patch" target="_blank">01-lib-patch.patch</a> 
<a href="SlickGrid-6Pac-Mar-2015-lib-update.zip" target="_blank">library files</a>
Update to jquery-1.11.2 and jquery-ui-1.11.3 (latest version as at Feb 2015)
- apply the patch
- extract the ZIP file
- replace the repo /css directory with the /css directory from the ZIP file
- add the files in the ZIP file /lib directory to the repo /lib directory 

<a href="02-dataview-bug.patch" target="_blank">02-dataview-bug.patch</a> Fix bug in dataview causing model benchmark test to throw an error




Recommended Patches
-------------------

These patches provide small, useful and non-breaking enhancements to mleibman/SlickGrid master

1. [SlickGrid-6pac-rec-01.pat](SlickGrid-6pac-rec-01.pat) Allow initialisation of SlickGrid when the parent element is hidden
