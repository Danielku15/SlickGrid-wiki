SlickGrid exposes the following events:

* onScroll
* onSort
* onHeaderContextMenu
* onHeaderClick
* onMouseEnter
* onMouseLeave
* onClick
* onDblClick
* onContextMenu
* onKeyDown
* onAddNewRow
* onValidationError
* onViewportChanged
* onColumnsReordered
* onColumnsResized
* onCellChange
* onBeforeEditCell
* onBeforeCellEditorDestroy
* onBeforeDestroy
* onActiveCellChanged
* onActiveCellPositionChanged
* onDragInit
* onDragStart
* onDrag
* onDragEnd
* onSelectedRowsChanged
* onInvalidatedRows

You can subscribe to the above events using a syntax similar to:

    gridInstance.onXYZEvent.subscribe(function(e,args){
        //event handling code.
    });
