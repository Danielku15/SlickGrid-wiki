SlickGrid exposes the following events:

* onScroll `({ scrollLeft: number, scrollTop: number })`  
* onSort `({ multiColumnSort: boolean, sortCol: Object, sortCols: Object[], sortAsc: boolean })`
* onHeaderContextMenu `({ column: Object })`
* onHeaderClick `({ column: Object })`
* onMouseEnter `({})`
* onMouseLeave `({})`
* onClick `({ row: number, cell: number })`
* onDblClick `({ row: number, cell: number })`
* onContextMenu `({})` 
* onKeyDown `({ row: number, cell: number })`
* onAddNewRow `({ item: any, column: Object })`
* onValidationError `({ editor: Object, cellNode: Object, validationResult: Object, row: number, cell: number, column: Object })`  
* onViewportChanged `({})`
* onColumnsReordered `({})`  
* onColumnsResized `({})`
* onCellChange `({ row: number, cell: number, item: any })` 
* onBeforeEditCell `({ row: number, cell: number, item: any, column: Object })` 
* onBeforeCellEditorDestroy `({ editor: Object })` 
* onHeaderCellRendered `({ node: Object, column: Object })`
* onHeaderRowCellRendered `({ node: Object, column: Object, grid: Object })`
* onBeforeHeaderCellDestroy `({ node: Object, column: Object })`
* onBeforeDestroy `({})`  
* onActiveCellChanged `({ row: number, cell: number }|null)`
* onActiveCellPositionChanged `({})`
* onDragInit
* onDragStart
* onDrag
* onDragEnd
* onSelectedRowsChanged `({ rows: number[] })`
* onCellCssStylesChanged `({ key: string, hash: Object })`

You can subscribe to the above events using a syntax similar to:

    gridInstance.onXYZEvent.subscribe(function(e, args){
        //event handling code.
    });

The handler is called with these arguments:  
e: Slick.EventData, which mimics the jQuery EventData.  
args: event specific data  

Event handlers can also be removed with

    gridInstance.onXYZEvent.unsubscribe(fn);
