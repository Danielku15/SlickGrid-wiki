Although the source of the [first example](http://mleibman.github.com/SlickGrid/examples/example1-simple.html) is self-explanatory, it's worth to point out the basics of SlickGrid. The following line

`var slickgrid = new Slick.Grid("#node", rows, columns, options);`

initializes -but doesn't display- SlickGrid, assigning its interface to the `slickgrid` var. Now we can use `slickgrid.someMethod()` in order to display the grid, pass data, listen to events...

**Node**

`"#node"` points to the HTML element where the grid should appear, typically being an empty `<div>`.

After we've passed `node`, `rows`, `columns` and `options` to `Slick.Grid`, we can proceed to display the grid.

`jQuery("#node").show();`

**Rows**

`rows` is an array of data objects. Example:

    var rows = [
        {
            field_1: "value1",
            field_2: "value2"
        }, {
            field_1: "value3",
            field_2: "value4"
        }
    ];

As it is passed passed by reference to the `Slick.Grid()` method, you can add, remove and sort its data objects without having to pass them again, but just refreshing SlickGrid's data model and view:

    slickgrid.updateRowCount();
    slickgrid.render();

The only exception to this is when deleting or replacing all data objects from `rows`:

    slickgrid.setData(rows); // Either a completely different array from the previously stored, or an empty array.
    slickgrid.updateRowCount();
    slickgrid.render();

**Columns**

`columns` is an array of objects, each being a column in the model, having at least the following fields:

* _name_ - The name to be displayed in the view.
* _field_ - The field name used in the data row objects.
* _id_ - An unique identifier for each column in the model, allowing to set more than one column reading the same field.

Example:

    var columns = [{
        name: "Address",
        field: "address"
        id: "address" // In most cases field and id will have the same value.
    }, 
    {
        name: "Rating, in %",
        field: "rating" // This and the following column read the same data, but can present it in a different way.
        id: "rating_percent"
    }, 
    {
        name: "Rating, in stars",
        field: "rating"
        id: "rating_stars"
    }];

**Options**

`enableCellNavigation: true` allows keyboard navigation. The `.active` CSS property defines the appearance of the currently selected cell.

These are all the currently available options:

    headerHeight
    rowHeight
    defaultColumnWidth
    enableAddRow
    leaveSpaceForNewRows
    editable
    autoEdit
    enableCellNavigation
    enableCellRangeSelection
    enableColumnReorder
    asyncEditorLoading
    asyncEditorLoadDelay
    forceFitColumns
    enableAsyncPostRender
    asyncPostRenderDelay
    autoHeight
    editorLock
    showHeaderRow
    headerRowHeight
    showTopPanel
    topPanelHeight
    formatterFactory
    editorFactory
    cellFlashingCssClass
    selectedCellCssClass
    multiSelect
    enableTextSelectionOnCells

**Events**

Most events are used like this:

    slickgrid.onDblClick.subscribe(function(e){           
        var cell = slickgrid.getCellFromEvent(e);
        var row = cell.row;
        var column_name = slickgrid.getColumns()[cell.cell].name);
        var column_field = slickgrid.getColumns()[cell.cell].field);
        var column_id = slickgrid.getColumns()[cell.cell].id);
    });

To date, the following events are available:

    onScroll        
    onSort          
    onHeaderContextMenu         
    onHeaderClick   
    onMouseEnter    
    onMouseLeave    
    onClick         
    onDblClick      
    onContextMenu   
    onKeyDown       
    onAddNewRow     
    onValidationError
    onViewportChanged
    onColumnsReordered          
    onColumnsResized
    onCellChange    
    onBeforeEditCell
    onBeforeCellEditorDestroy   
    onBeforeDestroy 
    onActiveCellChanged         
    onActiveCellPositionChanged 
    onDragInit      
    onDragStart     
    onDrag          
    onDragEnd       
    onSelectedRowsChanged

And it can be figured out by browsing the `handleDblClick`, `handleKeyDown`, etc, source, included in slick.grid.js.

**Basic sorting**

(doc pending)

**DataView**

It allows to sort and filter the data without modifying it.

(doc pending)