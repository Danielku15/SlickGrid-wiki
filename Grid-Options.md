As included in the examples or described in stable releases.

## Booleans:
* autoEdit _Cell will not automatically go into edit mode when selected._
* autoHeight 
* editable            
* enableAddRow _If true, a blank row will be displayed at the bottom - typing values in that row will add a new one._
* enableAsyncPostRender _If true, async post rendering will occur and asyncPostRender delegates on columns will be called._
* enableCellNavigation 
* enableColumnReorder                  
* enableRowReordering 
* forceFitColumns _Force column sizes to fit into the viewport (avoid horizontal scrolling)._
* showHeaderRow
* leaveSpaceForNewRows
* enableCellRangeSelection
* asyncEditorLoading _Makes cell editors load asynchronously after a small delay. This greatly increases keyboard navigation speed._
* multiSelect
* enableTextSelectionOnCells
* explicitInitialization (http://mleibman.github.com/SlickGrid/examples/example-explicit-initialization.html)
* multiColumnSort (http://mleibman.github.com/SlickGrid/examples/example-multi-column-sort.html)

## Others (with sample values)

* cellFlashingCssClass: "flashing" _A CSS class to apply to flashing cells via flashCell()._
* cellHighlightCssClass: "selected" _A CSS class to apply to cells highlighted via setHighlightedCells()._
* editCommandHandler: queueAndExecuteCommand
* rowHeight: 140
* topPanelHeight: 25
* defaultColumnWidth: 80
* asyncEditorLoadDelay: 100 _Delay after which cell editor is loaded. Ignored unless asyncEditorLoading is true._
* asyncPostRenderDelay: 60 _Delay after which async post renderer delegate is called._
* editorLock: _A Slick.EditorLock instance to use for controlling concurrent data edits._
* headerRowHeight: 25
* formatterFactory: _A factory object responsible to creating a formatter for a given cell. Must implement getFormatter(column)._
* editorFactory: _A factory object responsible to creating an editor for a given cell. Must implement getEditor(column)._