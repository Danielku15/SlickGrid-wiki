> [Wiki](Home) ▸ [[API Reference]] ▸ **Slick.Grid**

# Table of Contents

* <a href="#wiki-header-constructor">**Constructor**</a>
  * <a href="#wiki-constructor">new Slick.Grid</a>
* <a href="#wiki-header-core">**Core**</a>
  * <a href="#wiki-getData">getData</a>
  * <a href="#wiki-getDataItem">getDataItem</a>
  * <a href="#wiki-getSelectionModel">getSelectionModel</a>
  * <a href="#wiki-init">init</a>
  * <a href="#wiki-setData">setData</a>
  * <a href="#wiki-setOptions">setOptions</a>
* <a href="#wiki-header-columns">**Columns**</a>
  * <a href="#wiki-autosizeColumns">autosizeColumns</a>
  * <a href="#wiki-getColumnIndex">getColumnIndex</a>
  * <a href="#wiki-getColumns">getColumns</a>
  * <a href="#wiki-setSortColumn">setSortColumn</a>
  * <a href="#wiki-setSortColumns">setSortColumns</a>
  * <a href="#wiki-updateColumnHeader">updateColumnHeader</a>
* <a href="#wiki-header-cells">**Cells**</a>
  * <a href="#wiki-addCellCssStyles">addCellCssStyles</a>
  * <a href="#wiki-canCellBeActive">canCellBeActive</a>
  * <a href="#wiki-canCellBeSelected">canCellBeSelected</a>
  * <a href="#wiki-editActiveCell">editActiveCell</a>
  * <a href="#wiki-getActiveCell">getActiveCell</a>
  * <a href="#wiki-getCellEditor">getCellEditor</a>
  * <a href="#wiki-getCellFromEvent">getCellFromEvent</a>
  * <a href="#wiki-getCellFromPoint">getCellFromPoint</a>
  * <a href="#wiki-getCellNode">getCellNode</a>
  * <a href="#wiki-getCellNodeBox">getCellNodeBox</a>
  * <a href="#wiki-gotoCell">gotoCell</a>
  * <a href="#wiki-navigateDown">navigateDown</a>
  * <a href="#wiki-navigateLeft">navigateLeft</a>
  * <a href="#wiki-navigateNext">navigateNext</a>
  * <a href="#wiki-navigatePrev">navigatePrev</a>
  * <a href="#wiki-navigateRight">navigateRight</a>
  * <a href="#wiki-navigateUp">navigateUp</a>
  * <a href="#wiki-removeCellCssStyles">removeCellCssStyles</a>
  * <a href="#wiki-resetActiveCell">resetActiveCell</a>
  * <a href="#wiki-setActiveCell">setActiveCell</a>
  * <a href="#wiki-setCellCssStyles">setCellCssStyles</a>
* <a href="#wiki-header-rendering">**Rendering**</a>
  * <a href="#wiki-getCanvasNode">getCanvasNode</a>
  * <a href="#wiki-getRenderedRange">getRenderedRange</a>
  * <a href="#wiki-getViewport">getViewport</a>
  * <a href="#wiki-invalidate">invalidate</a>
  * <a href="#wiki-invalidateRow">invalidateRow</a>
  * <a href="#wiki-invalidateRows">invalidateRows</a>
  * <a href="#wiki-resizeCanvas">resizeCanvas</a>
  * <a href="#wiki-scrollCellIntoView">scrollCellIntoView</a>
  * <a href="#wiki-scrollRowIntoView">scrollRowIntoView</a>
  * <a href="#wiki-scrollRowToTop">scrollRowToTop</a>
  * <a href="#wiki-updateCell">updateCell</a>
  * <a href="#wiki-updateRow">updateRow</a>
  * <a href="#wiki-updateRowCount">updateRowCount</a>
* <a href="#wiki-header-headers">**Headers**</a>
  * <a href="#wiki-getHeaderRow">getHeaderRow</a>
  * <a href="#wiki-getHeaderRowColumn">getHeaderRowColumn</a>
  * <a href="#wiki-getSortColumns">getSortColumns</a>
  * <a href="#wiki-setHeaderRowVisibility">setHeaderRowVisibility</a>

# <a name="header-constructor" href="Slick.Grid#wiki-header-constructor">#</a> Constructor

<a name="constructor" href="Slick.Grid#wiki-constructor">#</a> var grid = new Slick.Grid(<i>container, data, columns, options</i>);

>`container` - Container node to create the grid in. This can be a DOM Element, a jQuery node, or a jQuery selector.
>
>`data` - Databinding source. This can either be a regular JavaScript array or a custom object exposing getItem(index) and getLength() functions.
>
>`columns` - An array of column definition objects.
>
>`options` - Additional options.

Create an instance of the grid.

# <a name="header-core" href="Slick.Grid#wiki-header-core">#</a> Core

<a name="getData" href="Slick.Grid#wiki-getData">#</a> grid.<b>getData</b>(<i></i>)

Returns an array of every data object, unless you're using `DataView` in whcih case it returns a DataView object.

<a name="getDataItem" href="Slick.Grid#wiki-getDataItem">#</a> grid.<b>getDataItem</b>(<i>index</i>)

>`index` - Item index.

Returns the databinding item at a given position.
```javascript
// Get the id of the 15th item
var id15 = grid.getDataItem(14).id;
```
<a name="getDataLength" href="Slick.Grid#wiki-getDataLength">#</a> grid.<b>getDataLength</b>(<i></i>)

Returns the size of the databinding source.
```javascript
// Create an array of just the ids from every data item
var ids = [];
for (var i=0; i<grid.getDataLength() ; i++) {
  ids.push(grid.getDataItem(i).id);
}
```
<a name="getOptions" href="Slick.Grid#wiki-getOptions">#</a> grid.<b>getOptions</b>(<i></i>)

Returns an object containing all of the Grid options set on the grid. [See a list of Grid Options here](https://github.com/mleibman/SlickGrid/wiki/Grid-Options).
```javascript
// Find all elements that are currently selected
var $selectedCells = $('.' + grid.getOptions().selectedCellCssClass);
```
<a name="getSelectedRows" href="Slick.Grid#wiki-getSelectedRows">#</a> grid.<b>getSelectedRows</b>(<i></i>)

Returns an array of row indices corresponding to the currently selected rows.

<a name="getSelectionModel" href="Slick.Grid#wiki-getSelectionModel">#</a> grid.<b>getSelectionModel</b>(<i></i>)

Returns the current SelectionModel. [See here for more information about SelectionModels](https://github.com/mleibman/SlickGrid/wiki/Handling-selection).

<a name="init" href="Slick.Grid#wiki-init">#</a> grid.<b>init</b>(<i></i>)

Initializes the grid. Called after plugins are registered.

<a name="setData" href="Slick.Grid#wiki-setData">#</a> grid.<b>setData</b>(<i>newData, scrollToTop</i>)

>`data` - New databinding source. This can either be a regular JavaScript array or a custom object exposing `getItem(index)` and `getLength()` functions.

>`scrollToTop` - If true, the grid will reset the vertical scroll position to the top of the grid. 

Sets a new source for databinding and removes all rendered rows.  Note that this doesn't render the new rows - you can follow it with a call to `render()` to do that.

<a name="setOptions" href="Slick.Grid#wiki-setOptions">#</a> grid.<b>setOptions</b>(<i>options</i>)

> `options` - An object with configuration options.

Extends grid options with a given hash. If an there is an active edit, the grid will attempt to commit the changes and only continue if the attempt succeeds.
```javascript
// set a new CSS class for selected cells
grid.setOptions( { selectedCellCssClass: "newSelection" } );

// Select the first row
grid.setSelectedRows([0]);

// get the elements for the selected cells
$('.newSelection');
```
<a name="setSelectedRows" href="Slick.Grid#wiki-setSelectedRows">#</a> grid.<b>setSelectedRows</b>(<i>rowsArray</i>)

> `rowsArray` - An array of row numbers.

Accepts an array of row indices and applies the current `selectedCellCssClass` to the cells in the row, respecting whether cells have been flagged as `selectable`.
```javascript
// Select the first three rows
grid.setSelectedRows([0, 1, 2]);
```
<a name="setSelectionModel" href="Slick.Grid#wiki-setSelectionModel">#</a> grid.<b>setSelectionModel</b>(<i>selectionModel</i>)

`selectionModel` - A [SelectionModel](https://github.com/mleibman/SlickGrid/wiki/Handling-selection).

Unregisters a current selection model and registers a new one. See [the definition of SelectionModel](https://github.com/mleibman/SlickGrid/wiki/Handling-selection) for more information.

# <a name="header-columns" href="Slick.Grid#wiki-header-columns">#</a> Columns
<a name="autosizeColumns" href="Slick.Grid#wiki-autosizeColumns">#</a> grid.<b>autosizeColumns</b>(<i></i>)

Proportionately resizes all columns to fill available horizontal space.  This does not take the cell contents into consideration.

<a name="getColumnIndex" href="Slick.Grid#wiki-getColumnIndex">#</a> grid.<b>getColumnIndex</b>(<i>id</i>)

>`id` - A column id.

Returns the index of a column with a given id.  Since columns can be reordered by the user, this can be used to get the column definition independent of the order:

```javascript
var column = grid.getColumns()[grid.getColumnIndex("title")]
```

<a name="getColumns" href="Slick.Grid#wiki-getColumns">#</a> grid.<b>getColumns</b>(<i></i>)

Returns an array of column definitions, containing the option settings for each individual column.
```javascript
// Log to console whether the first column is sortable
var cols = grid.getColumns();
var sortable = cols[0].sortable;
sortable ? console.log("It's sortable!") : console.log("It's not sortable!");
```
<a name="setColumns" href="Slick.Grid#wiki-setColumns">#</a> grid.<b>setColumns</b>(<i>columnDefinitions</i>)

>`columnDefinitions` - An array of column definitions.

Sets grid columns.  Column headers will be recreated and all rendered rows will be removed.  To rerender the grid (if necessary), call `render()`.
```javascript
// Change the name of the first column to "First"
var data = grid.getColumns();
data[0].name = "First";
grid.setColumns(data);
```

<a name="setSortColumn" href="Slick.Grid#wiki-setSortColumn">#</a> grid.<b>setSortColumn</b>(<i>columnId, ascending</i>)

Accepts a `columnId` string and an `ascending` boolean. Applies a sort glyph in either ascending or descending form to the header of the column. Note that this does _not_ actually sort the column. It only adds the sort glyph to the header.

<a name="setSortColumns" href="Slick.Grid#wiki-setSortColumns">#</a> grid.<b>setSortColumns</b>(<i>cols</i>)

Accepts an array of objects in the form `[ { columnId: [string], sortAsc: [boolean] }, ... ]`. When called, this will apply a sort glyph in either ascending or descending form to the header of each column specified in the array. Note that this does _not_ actually sort the column. It only adds the sort glyph to the header

<a name="updateColumnHeader" href="Slick.Grid#wiki-updateColumnHeader">#</a> grid.<b>updateColumnHeader</b>(<i>columnId, title, toolTip</i>)

>`id` - Column id.
>
> `title` - New column name.
>
> `toolTip` - New column tooltip.

Updates an existing column definition and a corresponding header DOM element with the new title and tooltip.
```javascript
// Change the column with an id of 'FirstName' to have the name "A First Name", and no tooltip.
grid.updateColumnHeader("FirstName", "A First Name");
```
# <a name="header-cells" href="Slick.Grid#wiki-header-cells">#</a> Cells

<a name="addCellCssStyles" href="Slick.Grid#wiki-addCellCssStyles">#</a> grid.<b>addCellCssStyles</b>(<i>key, hash</i>)

> `key` - A unique key you can use in calls to setCellCssStyles and removeCellCssStyles. If a hash with that key has already been set, an exception will be thrown.
>
>`hash` - A hash of additional cell CSS classes keyed by row number and then by column id. Multiple CSS classes can be specified and separated by space.
>
> Example:
>
>```javascript
{
    0:    {
        "number_column":    "cell-bold",
        "title_column":     "cell-title cell-highlighted"
    },
    4:    {
        "percent_column":    "cell-highlighted"
    }
}
>```

Adds an "overlay" of CSS classes to cell DOM elements. SlickGrid can have many such overlays associated with different keys and they are frequently used by plugins. For example, SlickGrid uses this method internally to decorate selected cells with selectedCellCssClass (see options).

<a name="canCellBeActive" href="Slick.Grid#wiki-canCellBeActive">#</a> grid.<b>canCellBeActive</b>(<i>row, col</i>)

>`row` - A row index.
>
>`col` - A column index.

Returns `true` if you can click on a given cell and make it the active focus.

<a name="canCellBeSelected" href="Slick.Grid#wiki-canCellBeSelected">#</a> grid.<b>canCellBeSelected</b>(<i>row, col</i>)

>`row` - A row index.
>
>`col` - A column index.

Returns `true` if selecting the row causes this particular cell to have the `selectedCellCssClass` applied to it. A cell can be selected if it exists and if it isn't on an empty / "Add New" row and if it is not marked as "unselectable" in the column definition.

<a name="editActiveCell" href="Slick.Grid#wiki-editActiveCell">#</a> grid.<b>editActiveCell</b>(<i>editor</i>)

>`editor` - A SlickGrid editor (see examples in `slick.editors.js`).

Attempts to switch the active cell into edit mode. Will throw an error if the cell is set to be not editable. Uses the specified `editor`, otherwise defaults to any default editor for that given cell.
```javascript
// Assuming slick.editors.js is included...
// Set the first cell in the first row to be active
grid.setActiveCell(0,0);

// Invoke the Date editor on that cell
grid.editActiveCell(Slick.Editors.Date);
```
<a name="flashCell" href="Slick.Grid#wiki-flashCell">#</a> grid.<b>flashCell</b>(<i>row, cell, speed</i>)

>`row` - A row index.
>
>`cell` - A column index.
>
>`speed` (optional) - The milliseconds delay between the toggling calls. Defaults to 100 ms.

Flashes the cell twice by toggling the CSS class 4 times.

<a name="getActiveCell" href="Slick.Grid#wiki-getActiveCell">#</a> grid.<b>getActiveCell</b>(<i></i>)

Returns an object representing the coordinates of the currently active cell:
```javascript
{
  row: activeRow, 
  cell: activeCell
}
```
<a name="getActiveCellNode" href="Slick.Grid#wiki-getActiveCellNode">#</a> grid.<b>getActiveCellNode</b>(<i></i>)

Returns the DOM element containing the currently active cell. If no cell is active, null is returned.
```javascript
// Get the element for the active cell
var $active = $(grid.getActiveCellNode())

// Add a new class to the active cell
$active.addClass('myClass');
```
<a name="getActiveCellPosition" href="Slick.Grid#wiki-getActiveCellPosition">#</a> grid.<b>getActiveCellPosition</b>(<i></i>)

Returns an object representing information about the active cell's position. All coordinates are absolute and take into consideration the visibility and scrolling position of all ancestors. The object takes the form:

```javascript
{ 
  bottom:  [numPixels],
  height:  [numPixels],
  left:    [numPixels], 
  right:   [numPixels], 
  top:     [numPixels], 
  visible: [boolean], 
  width:   [numPixels] 
}
```
<a name="getCellCssStyles" href="Slick.Grid#wiki-getCellCssStyles">#</a> grid.<b>getCellCssStyles</b>(<i>key</i>)

>`key` - A string.

Accepts a key name, returns the group of CSS styles defined under that name. See <a href="#wiki-setCellCssStyles">`setCellCssStyles`</a> for more info.

<a name="getCellEditor" href="Slick.Grid#wiki-getCellEditor">#</a> grid.<b>getCellEditor</b>(<i></i>)

Returns the active cell editor.  If there is no actively edited cell, null is returned.

<a name="getCellFromEvent" href="Slick.Grid#wiki-getCellFromEvent">#</a> grid.<b>getCellFromEvent</b>(<i>e</i>)

>`e` - A standard W3C/jQuery event.

Returns a hash containing row and cell indexes from a standard W3C/jQuery event.

<a name="getCellFromPoint" href="Slick.Grid#wiki-getCellFromPoint">#</a> grid.<b>getCellFromPoint</b>(<i>x, y</i>)

>`x` - An x coordinate.
>
>`y` - A y coordinate.

Returns a hash containing row and cell indexes. Coordinates are relative to the top left corner of the grid beginning with the first row (not including the column headers).

<a name="getCellNode" href="Slick.Grid#wiki-getCellNode">#</a> grid.<b>getCellNode</b>(<i>row, cell</i>)

>`row` - A row index.
>
>`cell` - A column index.

Returns a DOM element containing a cell at a given row and cell.

<a name="getCellNodeBox" href="Slick.Grid#wiki-getCellNodeBox">#</a> grid.<b>getCellNodeBox</b>(<i>row, cell</i>)

>`row` - A row index.
>
>`cell` - A column index.

Returns an object representing information about a cell's position. All coordinates are absolute and take into consideration the visibility and scrolling position of all ancestors. The object takes the form:

```javascript
{ 
  bottom:  [numPixels],
  height:  [numPixels],
  left:    [numPixels], 
  right:   [numPixels], 
  top:     [numPixels], 
  visible: [boolean], 
  width:   [numPixels] 
}
```

<a name="gotoCell" href="Slick.Grid#wiki-gotoCell">#</a> grid.<b>gotoCell</b>(<i>row, cell, forceEdit</i>)

Accepts a `row` integer and a `cell` integer, scrolling the view to the row where `row` is its row index, and `cell` is its cell index. Optionally accepts a `forceEdit` boolean which, if true, will attempt to initiate the edit dialogue for the field in the specified cell.

Unlike `setActiveCell`, this scrolls the row into the viewport and sets the keyboard focus.

<a name="navigateDown" href="Slick.Grid#wiki-navigateDown">#</a> grid.<b>navigateDown</b>(<i></i>)

Switches the active cell one row down skipping unselectable cells. Returns a boolean saying whether it was able to complete or not.

<a name="navigateLeft" href="Slick.Grid#wiki-navigateLeft">#</a> grid.<b>navigateLeft</b>(<i></i>)

Switches the active cell one cell left skipping unselectable cells.  Unline `navigatePrev`, `navigateLeft` stops at the first cell of the row. Returns a boolean saying whether it was able to complete or not.

<a name="navigateNext" href="Slick.Grid#wiki-navigateNext">#</a> grid.<b>navigateNext</b>(<i></i>)

Tabs over active cell to the next selectable cell. Returns a boolean saying whether it was able to complete or not.

<a name="navigatePrev" href="Slick.Grid#wiki-navigatePrev">#</a> grid.<b>navigatePrev</b>(<i></i>)

Tabs over active cell to the previous selectable cell. Returns a boolean saying whether it was able to complete or not.

<a name="navigateRight" href="Slick.Grid#wiki-navigateRight">#</a> grid.<b>navigateRight</b>(<i></i>)

Switches the active cell one cell right skipping unselectable cells.  Unline `navigateNext`, `navigateRight` stops at the last cell of the row. Returns a boolean saying whether it was able to complete or not.

<a name="navigateUp" href="Slick.Grid#wiki-navigateUp">#</a> grid.<b>navigateUp</b>(<i></i>)

Switches the active cell one row up skipping unselectable cells. Returns a boolean saying whether it was able to complete or not.

<a name="removeCellCssStyles" href="Slick.Grid#wiki-removeCellCssStyles">#</a> grid.<b>removeCellCssStyles</b>(<i>key</i>)

>`key` - A string key.

Removes an "overlay" of CSS classes from cell DOM elements.  See <a href="#wiki-setCellCssStyles">`setCellCssStyles`</a> for more.

<a name="resetActiveCell" href="Slick.Grid#wiki-resetActiveCell">#</a> grid.<b>resetActiveCell</b>(<i></i>)

Resets active cell.

<a name="setActiveCell" href="Slick.Grid#wiki-setActiveCell">#</a> grid.<b>setActiveCell</b>(<i>row, cell</i>)

>`row` - A row index.
>
>`cell` - A column index.

Sets an active cell.

<a name="setCellCssStyles" href="Slick.Grid#wiki-setCellCssStyles">#</a> grid.<b>setCellCssStyles</b>(<i>key, hash</i>)

> `key` - A string key. Will overwrite any data already associated with this key.
>
>`hash` - A hash of additional cell CSS classes keyed by row number and then by column id. Multiple CSS classes can be specified and separated by space.
>
> Example:
>
>```javascript
{
    0:    {
        "number_column":    "cell-bold",
        "title_column":     "cell-title cell-highlighted"
    },
    4:    {
        "percent_column":    "cell-highlighted"
    }
}
>```

Sets CSS classes to specific grid cells by calling `removeCellCssStyles(key)` followed by `addCellCssStyles(key, hash)`. `key` is name for this set of styles so you can reference it later - to modify it or remove it, for example. `hash` is a per-row-index, per-column-name nested hash of CSS classes to apply.

Suppose you have a grid with columns:

["login", "name", "birthday", "age", "likes_icecream", "favorite_cake"]

...and you'd like to highlight the "birthday" and "age" columns for people whose birthday is today, in this case, rows at index 0 and 9. (The first and tenth row in the grid).

```css
   .highlight{ background: yellow } 
```

```javascript
grid.setCellCssStyles("birthday_highlight", {
   0: {
        birthday: "highlight", 
        age: "highlight" 
       },

   9: {
         birthday: "highlight",
         age: "highlight"
       }
})
```

# <a name="header-rendering" href="Slick.Grid#wiki-header-rendering">#</a> Rendering
<a name="getCanvasNode" href="Slick.Grid#wiki-getCanvasNode">#</a> grid.<b>getCanvasNode</b>(<i></i>)

Returns the DIV element matching class `grid-canvas`, which contains every data row currently being rendered in the DOM.
```javascript
// Get the total number of data rows being rendered in the DOM.
var numRenderedRows = $(grid.getCanvasNode()).children().length;
```
<a name="getGridPosition" href="Slick.Grid#wiki-getGridPosition">#</a> grid.<b>getGridPosition</b>(<i></i>)

Returns an object representing information about the grid's position on the page. The object takes the form:

```javascript
{ 
  bottom:  [numPixels],
  height:  [numPixels],
  left:    [numPixels], 
  right:   [numPixels], 
  top:     [numPixels], 
  visible: [boolean], 
  width:   [numPixels] 
}
```

<a name="getRenderedRange" href="Slick.Grid#wiki-getRenderedRange">#</a> grid.<b>getRenderedRange</b>(<i>viewportTop, viewportLeft</i>)

>`viewportTop` (optional) - The number of pixels offset from the top of the grid.
>
>`viewportLeft` (optional) - The number of pixels offset from the left of the grid.

If passed no arguments, returns an object that tells you the range of rows (by row number) currently being rendered, as well as the left/right range of pixels currently rendered. `{ top: [rowIndex], bottom: [rowIndex], leftPx: [numPixels], rightPx: [numPixels] }`

The options `viewportTop` and `viewportLeft` are optional, and tell what what would be rendered at a certain scroll top/left offset. For example, `grid.getRenderedRange(1000)` would essentially be asking: "if I were to scroll 1000 pixels down, what rows would be rendered?"

<a name="getViewport" href="Slick.Grid#wiki-getViewport">#</a> grid.<b>getViewport</b>(<i>viewportTop, viewportLeft</i>)

>`viewportTop` (optional) - The number of pixels offset from the top of the grid.
>
>`viewportLeft` (optional) - The number of pixels offset from the left of the grid.

Returns an object telling you which rows are currently being displayed on the screen, and also the pixel offsets for left/right scrolling. `{ top: [rowIndex], bottom: [rowIndex], leftPx: [numPixels], rightPx: [numPixels] }`

Also accepts `viewportTop` and `viewportLeft` offsets to tell you what would be shown to the user if you were to scroll to that point.

<a name="invalidate" href="Slick.Grid#wiki-invalidate">#</a> grid.<b>invalidate</b>(<i></i>)

Redraws the grid. Invalidates all rows and calls `render()`.
```javascript
// Change the name property of the first row
var data = grid.getData();
data[0].name = "New name!"

// Call invalidate to render the data again. No need to call render, as this calls it for you.
grid.invalidate();
```
<a name="invalidateAllRows" href="Slick.Grid#wiki-invalidateAllRows">#</a> grid.<b>invalidateAllRows</b>(<i></i>)

Tells the grid that all rows in the table are invalid. (If `render()` is called after this, it will redraw the entire grid.)

<a name="invalidateRow" href="Slick.Grid#wiki-invalidateRow">#</a> grid.<b>invalidateRow</b>(<i>row</i>)

> `row` - A row index.

Tells the grid that the row specified by `row` is invalid. (If `render()` is called after this, it will redraw the contents of that row.)

<a name="invalidateRows" href="Slick.Grid#wiki-invalidateRows">#</a> grid.<b>invalidateRows</b>(<i>rows</i>)

> `rows` - An array of row indices.

Accepts an array of row indices, and tells the grid that those rows are invalid. (If `render()` is called after this, it will redraw the contents of those rows.)
```javascript
// Change the name property of the first row
var data = grid.getData();
data[0].name = "New name!"
data[1].name = "Another new name!"

// Call invalidateRows to invalidate the first two rows
grid.invalidateRows([0,1]);

// Call render to render them again
grid.render();
```
<a name="render" href="Slick.Grid#wiki-render">#</a> grid.<b>render</b>(<i></i>)

Rerenders rows in the DOM.

<a name="resizeCanvas" href="Slick.Grid#wiki-resizeCanvas">#</a> grid.<b>resizeCanvas</b>(<i></i>)

Resizes the canvas to fit the current DIV container. (For example, to resize the grid, you would first change the size of the div, then call `resizeCanvas()`.)

<a name="scrollCellIntoView" href="Slick.Grid#wiki-scrollCellIntoView">#</a> grid.<b>scrollCellIntoView</b>(<i>row, cell</i>)

>`row` - A row index.
>
>`cell` - A column index.

Scrolls the indicated cell into view.

Note that this does nothing unless the indicated column is already not in view. For example, if the grid is scrolled to the far left and you were looking at row 0, calling `scrollCellIntoView(100,0)` would not simply scroll you to row 100. But if column 8 were out of view and you called `scrollCellIntoView(100,8)`, then it would scroll down and to the right.

<a name="scrollRowIntoView" href="Slick.Grid#wiki-scrollRowIntoView">#</a> grid.<b>scrollRowIntoView</b>(<i>row, doPaging</i>)

>`row` - A row index.
>
>`doPaging` - A boolean. If `false`, the grid will scroll so the indicated row is at the top of the view. If `true`, the grid will scroll so the indicated row is at the bottom of the view. Defaults to `false`.

Scrolls the view to the indicated row.

<a name="scrollRowToTop" href="Slick.Grid#wiki-scrollRowToTop">#</a> grid.<b>scrollRowToTop</b>(<i>row</i>)

>`row` - A row index.

Scrolls the view to the indicated row, placing the row at the top of the view.

<a name="updateCell" href="Slick.Grid#wiki-updateCell">#</a> grid.<b>updateCell</b>(<i>row, cell</i>)

TODO
```javascript
// put stuff here
```

<a name="updateRow" href="Slick.Grid#wiki-updateRow">#</a> grid.<b>updateRow</b>(<i>row</i>)

TODO
```javascript
// put stuff here
```

<a name="updateRowCount" href="Slick.Grid#wiki-updateRowCount">#</a> grid.<b>updateRowCount</b>(<i></i>)

TODO
```javascript
// put stuff here
```

# <a name="header-headers" href="Slick.Grid#wiki-header-headers">#</a> Headers

<a name="getHeaderRow" href="Slick.Grid#wiki-getHeaderRow">#</a> grid.<b>getHeaderRow</b>(<i></i>)

Returns the element of a DIV row beneath the actual column headers. For an example of how you might use this, see the [header row quick filter example](http://mleibman.github.com/SlickGrid/examples/example-header-row.html), which grabs the element, appends inputs, and delegates events to the inputs.

<a name="getHeaderRowColumn" href="Slick.Grid#wiki-getHeaderRowColumn">#</a> grid.<b>getHeaderRowColumn</b>(<i>columnId</i>)

>`columnId` - The `id` string of a column.

If a header row is implemented and has one child for each column, as seen in the [header row quick filter example](http://mleibman.github.com/SlickGrid/examples/example-header-row.html), you may use this function to pass a columnId and get the individual cell from that header row. Returns a DIV element.

<a name="getSortColumns" href="Slick.Grid#wiki-getSortColumns">#</a> grid.<b>getSortColumns</b>(<i></i>)

Returns an array of objects representing columns that have a sort glyph in the header: 
```javascript
{ 
  columnId: [string],
  sortAsc:  [boolean]
}
```
<a name="getTopPanel" href="Slick.Grid#wiki-getTopPanel">#</a> grid.<b>getTopPanel</b>(<i></i>)

Returns the DIV element of the top panel. The panel is hidden by default, but you can show it by initializing the grid with `showTopPanel` set to `true`, or by calling `grid.setTopePanelVisibility(true)`.
```javascript
// Create a subheader and attach it to the top panel
$("<div>Here is a subheader!</div>")
  .appendTo(grid.getTopPanel());
// Show the top panel
grid.setTopPanelVisibility(true);
```

<a name="setHeaderRowVisibility" href="Slick.Grid#wiki-setHeaderRowVisibility">#</a> grid.<b>setHeaderRowVisibility</b>(<i>visible</i>)

TODO
```javascript
// put stuff here
```