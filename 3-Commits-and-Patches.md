# Commit and patch list

You can check out the commits in the repo, and remember, [6pac/SlickGrid](https://github.com/6pac/SlickGrid) is an up-to-date, ready-to-download version of SlickGrid.
However, if you have forked your repo and made changes, then you may want to apply patches piecemeal.

This page lists one patch per commit.

***

<a href="01-lib-patch.patch" target="_blank">01-lib-patch.patch</a> <a href="01-lib-patch.zip" target="_blank">01-lib-patch.zip</a>
Update to jquery-1.11.2 and jquery-ui-1.11.3 (latest version as at Feb 2015)
- apply the patch
- extract the ZIP file
- replace the repo /css directory with the /css directory from the ZIP file
- add the files in the ZIP file /lib directory to the repo /lib directory 

<a href="02-dataview-bug.patch" target="_blank">02-dataview-bug.patch</a> Fix bug in dataview causing model benchmark test to throw an error

<a href="03-redundant-pager-code.patch" target="_blank">03-redundant-pager-code.patch</a> Remove redundant slick pager code

<a href="04-fract-pixel-width.patch" target="_blank">04-fract-pixel-width.patch</a> Fix unnecessary horizontal scroll for autosized columns when viewport has fractional pixel width

<a href="05-default-comparer.patch" target="_blank">05-default-comparer.patch</a> Make default group comparer function more robust - see pull request: fix sort order in Chrome #1019

<a href="06-single-stylesheet.patch" target="_blank">06-single-stylesheet.patch</a> use a single stylesheet when multiple grids are instantiated, rather than creating one for each grid. thanks to bdwidhalm: mleibman#955

<a href="07-fix-grouping-bug.patch" target="_blank">07-fix-grouping-bug.patch</a> fix grouping bug (fix issue #841 & #896 mleibman#898)

<a href="08-dataview-regex.patch" target="_blank">08-dataview-regex.patch</a> update DataView compiled-expression regex to deal with some forms of minification.

Minification can remove semicolons, add or remove braces, stc. RegEx is never going to be able to solve all use cases so filter functions should be designed with compilation in mind.
Filter functions can also be declared in a separate non-minified script block or file.

Issues:
- mleibman#301
- mleibman#244
- mleibman#1032
- mleibman#1053
- http://stackoverflow.com/questions/27702628/script-minified-with-bundling-dont-work-in-asp-net-mvc-3-when-debugging-is-disa

<a href="09-fix-ajax.patch" target="_blank">09-fix-ajax.patch</a> Fix Issue #963 ajax example not working
- add Rand Scullard's pull request mleibman#975 as the new example-6-ajax-loading.html

<a href="10-ajax-yahoo.patch" target="_blank">10-ajax-yahoo.patch</a> additional version of ajax loading page, using Yahoo news and YQL as a source. the format of the grid rows is more in keeping with the newsfeed style of the original

<a href="11-hidden-init-css.patch" target="_blank">11-hidden-init-css.patch</a> Allow initialisation of hidden Grid
- add css manipulation so that grid initialises successfully if the parent element is hidden

<a href="12-retarget-demo-links.patch" target="_blank">12-retarget-demo-links.patch</a> update go-to-source links to 6pac repo master branch


