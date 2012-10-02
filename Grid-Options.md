As included in the examples or described in stable releases.

## Booleans with defaults
* asyncEditorLoading: **false**; (Makes cell editors load asynchronously after a small delay. This greatly increases keyboard navigation speed.)
* autoEdit: **true**; (Cell will not automatically go into edit mode when selected.)
* autoHeight: **false**;
* editable: **false**;
* enableAddRow: **false**; (If true, a blank row will be displayed at the bottom - typing values in that row will add a new one.)
* enableAsyncPostRender: **false**; (If true, async post rendering will occur and asyncPostRender delegates on columns will be called.)
* enableCellRangeSelection: **null**;
* enableCellNavigation: **true**;
* enableColumnReorder: **true**;
* enableRowReordering: **null**;
* enableTextSelectionOnCells: **false**;
* forceFitColumns: **false** (Force column sizes to fit into the viewport (avoid horizontal scrolling).)
* leaveSpaceForNewRows: **false**;
* multiSelect: **true**;
* explicitInitialization: **false**; (http://mleibman.github.com/SlickGrid/examples/example-explicit-initialization.html)
* multiColumnSort: **false**; (http://mleibman.github.com/SlickGrid/examples/example-multi-column-sort.html)
* showHeaderRow: **false**;

## Others with sample values
* asyncPostRenderDelay: **60**; (Delay after which async post renderer delegate is called.)
* asyncEditorLoadDelay: **100**; (Delay after which cell editor is loaded. Ignored unless asyncEditorLoading is true.)
* cellFlashingCssClass: "flashing"; (A CSS class to apply to flashing cells via flashCell().)
* cellHighlightCssClass: "selected"; (A CSS class to apply to cells highlighted via setHighlightedCells().)
* defaultColumnWidth: 80;
* editCommandHandler: queueAndExecuteCommand;
* editorFactory: **null**; (A factory object responsible to creating an editor for a given cell. Must implement getEditor(column).)
* editorLock: **Slick.GlobalEditorLock**; (A Slick.EditorLock instance to use for controlling concurrent data edits.)
* formatterFactory: **null**; (A factory object responsible to creating a formatter for a given cell. Must implement getFormatter(column).)
* headerRowHeight: **25**;
* rowHeight: **140**;
* topPanelHeight: **25**;