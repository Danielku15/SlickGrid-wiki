# Patch List

The following are the bug fixes (most recent first) made since forking from the main MLeibman branch, a significant number 
in response to issues or pull requests.

* breaking change: updated jquery.event.drag-2.2.js and jquery.event.drop-2.2.js to be compatible with jQuery 3, bumped these to jquery.event.drag-2.3.0.js and jquery.event.drop-2.3.0.js
* tested with jQuery 1.8.3, 1.11.2, 2.2.4, and 3.1.0  -- thanks to lfilho
* updated repo to work with jQuery 3.x (without needing jQuery-Migrate) -- thanks to lfilho
* fix bug with refresh last row of grid
* fix bug in compound editor example 'isValueChanged' method
* add internal keycode enums instead of hadcoded key codes
* fix error in autotooltips test
* remove deprecated jquery .browser property
* fix bugs identified by JsHint
* Patch absBox for null element bug (MLeibman #1066)
* Fix column resizing issues with Bootstrap 3/box-sizing:border-box
* Fix jQueryUI css interfering with SlickGrid css issues
* Prevent useless onSelectedRangesChanged events in selectionmodels' setSelectedRanges
* Fix tooltip error with draggable columns 
* additional version of ajax loading page, using Yahoo news and YQL as a source. the format of the grid rows is more in keeping with the newsfeed style of the original
* Fix Issue #963 ajax example not working
* update DataView compiled-expression regex to deal with some forms of minification
    Minification can remove semicolons, add or remove braces, etc. RegEx is never going to be able to solve all use cases so filter functions should be designed with compilation in mind.
    Filter functions can also be declared in a separate non-minified script block or file.
    Issues:
    - mleibman#301, mleibman#244, mleibman#1032, mleibman#1053
    - http://stackoverflow.com/questions/27702628/script-minified-with-bundling-dont-work-in-asp-net-mvc-3-when-debugging-is-disa
* fix grouping bug (issue #841 & #896 mleibman#898)
* Make default group comparer function more robust (issue mleibman#1019)
* Fix unnecessary horizontal scroll for autosized columns when viewport has fractional pixel width
* Remove redundant slick pager code
* Fix bug in dataview causing model benchmark test to throw an error
* update to jquery-1.11.2 and jquery-ui-1.11.3, with minor patches to accommodate the change
