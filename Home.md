# SlickGrid Current Master Repository

NEW SlickGrid Website! https://slickgrid.net/

[download the latest SlickGrid official release](https://github.com/6pac/SlickGrid/releases)  
[download the latest repo version](https://github.com/6pac/SlickGrid)

*** NEWS FLASH ***
The frozen column and row code has been integrated into this repo from the X-Slickgrid and JLynch repos.

This is the acknowledged current master repository for SlickGrid since the MLeibman branch ceased being maintained.
It builds on the current state of the mleibman/SlickGrid master branch, keeping libraries up to date and applying small,
safe core patches and enhancements _without_ turning into a personalised build. 

Check out the sidebar menu to the right for the wiki contents.

Check out the [examples](https://github.com/6pac/SlickGrid/wiki/Examples) for examples demonstrating new features and use cases, such as dynamic grid creation and editors with third party controls.

Do you use SlickGrid? Add your site to the [[Used By]]!

Want to show your appreciation?  Hit "Donate!" [here](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=michael%2eleibman%40gmail%2ecom&lc=US&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donateCC_LG%2egif%3aNonHosted)

<h2>What it is</h2>

Quite simply, SlickGrid is a JavaScript grid/spreadsheet component.
It is an advanced component and is going to be a bit more difficult to learn and configure, but once you realize its full potential, it will blow your mind!

Some highlights:

* Adaptive virtual scrolling (handle hundreds of thousands of rows with extreme responsiveness)
* Extremely fast rendering speed
* Supports jQuery UI Themes
* Background post-rendering for richer cells
* Configurable & customizable
* Column resize/reorder/show/hide
* Column autosizing & force-fit
* Pluggable cell formatters & editors
* Support for editing and creating new rows.
* Grouping, filtering, custom aggregators, and more!
* Advanced detached & multi-field editors with undo/redo support.
* "GlobalEditorLock" to manage concurrent edits in cases where multiple Views on a page can edit the same data. 

<h2>Resources</h2>

<h3>Dependencies</h3>

* jQuery
* jQueryUI Sortable (optional, only if column reordering is enabled)
* jquery.event.drag - http://threedubmedia.com/code/event/drag
* jquery.event.drop - http://threedubmedia.com/code/event/drop  
 (the ThreeDub Media drag and drop libraries have been updated to support jQuery 1.x, 2.x and 3.x and have been updated to v2.3. this update was made by this project and is not supported externally)

<h3>Documentation</h3>

* [[Getting Started]] - A brief introduction to some of SlickGrid's basic concepts.
* [Examples](https://github.com/6pac/SlickGrid/wiki/Examples) - A broad set of examples that demonstrate the most effective ways of using SlickGrid (probably the best place to learn how to use it).
* [API Reference](https://github.com/6pac/SlickGrid/wiki/API-Reference)
* [[Handling selection]]
* [All pages on this wiki](https://github.com/6pac/SlickGrid/wiki/_pages)

<h3>Contact/Support</h3>

**GitHub Issues are for bug reports only. Please use the appropriate forum.**
[Please see Rules of conduct](https://github.com/6pac/SlickGrid/wiki/Rules-of-conduct)

* Asking questions
    * [SlickGrid questions on StackOverflow](http://stackoverflow.com/questions/tagged/slickgrid)

* Reporting bugs
    * [SlickGrid GitHub issues page](https://github.com/6pac/SlickGrid/issues)

When reporting bugs, please be specific (details are described in the above "Rules of conduct"):

1. Include the version of SlickGrid.
2. Start with an existing example and customise it as sparingly as possible to reproduce the problem. Include the reproduction steps. Describe expected behavior & actual behavior. 
3. Use proper English that everybody can understand.

<h2>What makes it different</h2>

<h3>Virtual rendering</h3>

SlickGrid utilizes virtual rendering to enable you to easily work with hundreds of thousands of items without any drop in performance. In fact, there is no difference in performance between working with a grid with 10 rows versus a 100'000 rows. This is achieved through virtual rendering where only what's visible on the screen plus a small buffer is rendered. As the user scrolls, DOM nodes are continuously being created and removed. These operations are highly tuned to provide optimal performance under all browsers. The grid also adapts to the direction and speed of scroll to minimize the number of rows that need to be swapped out and to dynamically switch between synchronous and asynchronous rendering.

It does a few other things to maximize performance, such as dynamically generating and updating CSS rules, so that resizing a column does not change the grid DOM tree and only causes one reflow, and loading cell editors asynchronously to maximize keyboard navigation speed.

<h3>Grid vs Data</h3>

The key difference is between SlickGrid and other grid implementation I have seen is that they focus too much on being able to understand and work with data (search, sort, parse, ajax load, etc.) and not enough on being a better "grid" (or, in case of editable grids, a spreadsheet). It's great if all you want to do is "spruce up" an HTML TABLE or slap a front end onto a simple list, but too inflexible for anything else.

Data is complicated. It has business rules. It has non-intrinsic properties. Editing one property of an element can lead to cascading changes modifying other properties or even other elements. It has dependencies. What I'm saying, is that dealing with data is best left to the developer using the grid control. Trying to fit all of that into the grid implementation and API will only limit its applicability and add considerable bloat.

SlickGrid takes a different approach. In the simplest scenario, it accesses data through an array interface (i.e. using "dataitem" to get to an item at a given position and "data.length" to determine the number of items), but the API is structured in such a way that it is very easy to make the grid react to any possible changes to the underlying data. 

<h3>Responding to data source changes</h3>

While this may not be immediately obvious from what you see in the examples and in the code, the key use of the grid is in MVC applications where the grid is wired to respond to events in the Model.  In our application we have spreadsheet component of a Gantt chart, and the Model is a "filtered" view of the tasks (rows) in the original datasource.  Suppose you collapse or expand a parent task or enter some text in a Quick Filter textbox.  The Model then recalculates which rows are now visible, compares that with what was visible before and fires two events - onRowCountChanged & onRowsChanged.  The latter one tells all subscribed Views, such as the grid, that the rows in specific positions changed.  The grid then only has to invalidate/remove those rows and call grid.renderViewport() to make sure that whatever is in the viewport is visible.  The onRowCountChanged event triggers the recalculation of the virtual canvas - grid.resizeCanvas().  Together, this pattern makes for an incredibly efficient, flexible and, most importantly, scalable implementation. 


<h2>Unsupported browsers</h2>
Rather than listing all the browsers that SlickGrid works on, I will concentrate on the ones that don't.  

IE6 is explicitly NOT supported.  While some people have made SlickGrid work with IE6, I am not going to merge those changes in or spend any time testing on IE6 and trying to make it work.  If you have to support it, I feel your pain, but I don't want to share it.
