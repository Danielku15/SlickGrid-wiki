Options which you can apply to the columns objects.

| Option | Default | Description 
|------- | ------- | ----------- 
|asyncPostRender| null | This accepts a function of the form ```function(cellNode, row, dataContext, colDef)``` and is used to post-process the cell's DOM node / nodes
| behavior | null | Used by the the slick.rowMoveManager.js plugin for moving rows. Has no effect without the plugin installed.
| cannotTriggerInsert | null | In the "Add New" row, determines whether clicking cells in this column can trigger row addition. If true, clicking on the cell in this column in the "Add New" row will not trigger row addition.
| cellAttrs | null | Applies custom attributes to the DIV of every row cell in the column. Accepts an object in the form of `{'col-id': colDef.id}` |
| cssClass | "" | Accepts a string as a class name, applies that class to every row cell in the column. |
| defaultSortAsc | true | When set to ```true```, the first user click on the header will do an ascending sort. When set to ```false```, the first user click on the header will do an descending sort. |
| editor | null | The editor for cell edits (TextEditor, IntegerEditor, DateEditor...) See [slick.editors.js](https://github.com/6pac/SlickGrid/blob/master/slick.editors.js) |
| field | "" | The property name in the data object to pull content from. (This is assumed to be on the root of the data object.) |
| focusable | true | When set to ```false```, clicking on a cell in this column will not select the row for that cell. The cells in this column will also be skipped during tab navigation.|
| formatter | null | This accepts a function of the form ```function(row, cell, value, columnDef, dataContext)``` and returns a formatted version of the data in each cell of this column. The output can be eiher plain text or an object { text, removeClasses, addClasses, toolTip }. For example, setting ```formatter``` to ```function(r, c, v, cd, dc) { return "Hello!"; }``` would overwrite every value in the column with "Hello!" More information about different kinds of formatters can be found in the [example2](https://github.com/6pac/SlickGrid/blob/master/examples/example2-formatters.html) source code.
| headerCellAttrs | null | Applies custom attributes to the cell for the column header. Accepts an object in the form of `{'col-id': colDef.id}` |
| headerCssClass | null | Accepts a string as a class name, applies that class to the cell for the column header. |
| id | "" | A unique identifier for the column within the grid. |
| maxWidth | null | Set the maximum allowable width of this column, in pixels. |
| minWidth | 30 | Set the minimum allowable width of this column, in pixels. |
| name | "" | The text to display on the column heading. |
| rerenderOnResize | false | If set to true, whenever this column is resized, the entire table view will rerender. |
| resizable | true | If ```false```, column can no longer be resized. |
| selectable | true | If ```false```, when a row is selected, the CSS class for selected cells ("selected" by default) is not applied to the cell in this column. |
| sortable | false | If ```true```, the column will be sortable by clicking on the header. |
| toolTip | "" | If set to a non-empty string, a tooltip will appear on hover containing the string. |
| width || Width of the column in pixels. (May often be overridden by things like minWidth, maxWidth, forceFitColumns, etc.) |