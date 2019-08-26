SlickGrid exposes the following events:

* onActiveCellChanged `({ row: number, cell: number }|null)`
* onActiveCellPositionChanged `({})`
* onAddNewRow `({ item: any, column: Object })`
* onBeforeCellEditorDestroy `({ editor: Object })` 
* onBeforeDestroy `({})`  
* onBeforeEditCell `({ row: number, cell: number, item: any, column: Object })` 
* onBeforeHeaderCellDestroy `({ node: Object, column: Object })`
* onCellChange `({ row: number, cell: number, item: any })` 
* onCellCssStylesChanged `({ key: string, hash: Object })`
* onClick `({ row: number, cell: number })`
* onColumnsReordered `({})`  
* onColumnsResized `({triggeredByColumn: string})`
* onContextMenu `({})` 
* onDblClick `({ row: number, cell: number })`
* onDrag
* onDragEnd
* onDragInit
* onDragStart
* onFooterClick `({ column: Object })`
* onFooterContextMenu `({ column: Object })`
* onHeaderCellRendered `({ node: Object, column: Object })`
* onHeaderClick `({ column: Object })`
* onHeaderContextMenu `({ column: Object })`
* onHeaderRowCellRendered `({ node: Object, column: Object, grid: Object })`
* onKeyDown `({ row: number, cell: number })`
* onMouseEnter `({})`
* onMouseLeave `({})`
* onScroll `({ scrollLeft: number, scrollTop: number })`  
* onSelectedRowsChanged `({ rows: number[] })`
* onSort `({ multiColumnSort: boolean, sortCol: Object, sortCols: Object[], sortAsc: boolean })`
* onValidationError `({ editor: Object, cellNode: Object, validationResult: Object, row: number, cell: number, column: Object })`  
* onViewportChanged `({})`


You can subscribe to the above events using a syntax similar to:

    gridInstance.onXYZEvent.subscribe(function(e, args){
        //event handling code.
    });

The handler is called with these arguments:  
e: Slick.EventData, which mimics the jQuery EventData.  
args: event specific data  

Event handlers can also be removed with

    gridInstance.onXYZEvent.unsubscribe(fn);
