As included in the examples or described in stable releases:

| Option | Default | Description |
|------- | ------- | ----------- |
| asyncEditorLoading | false | Makes cell editors load asynchronously after a small delay. This greatly increases keyboard navigation speed.|
| asyncEditorLoadDelay|100|Delay after which cell editor is loaded. Ignored unless asyncEditorLoading is true.|
| asyncPostRenderDelay | 50 ||
| autoEdit | true | Cell will not automatically go into edit mode when selected.|
| autoHeight | false | This disables vertical scrolling. |
| cellFlashingCssClass|"flashing"|A CSS class to apply to flashing cells via flashCell().|
| cellHighlightCssClass|"selected"|A CSS class to apply to cells highlighted via setHighlightedCells().|
| dataItemColumnValueExtractor | null ||
| defaultColumnWidth|80||
| defaultFormatter | defaultFormatter ||
| editable | false ||
| editCommandHandler | queueAndExecuteCommand | _Not listed as a default under options in slick.grid.js_ |
| editorFactory | null | A factory object responsible to creating an editor for a given cell. Must implement getEditor(column). |
| editorLock | Slick.GlobalEditorLock | A Slick.EditorLock instance to use for controlling concurrent data edits. |
| enableAddRow | false | If true, a blank row will be displayed at the bottom - typing values in that row will add a new one. Must subscribe to onAddNewRow to save values. |
| enableAsyncPostRender | false | If true, async post rendering will occur and asyncPostRender delegates on columns will be called. |
| enableCellRangeSelection | null| **WARNING**: Not contained in SlickGrid 2.1, may be deprecated |
| enableCellNavigation | true | Appears to enable cell virtualisation for optimised speed with large datasets |
| enableColumnReorder | true||
| enableRowReordering | null| **WARNING**: Not contained in SlickGrid 2.1, may be deprecated |
| enableTextSelectionOnCells | false||
| explicitInitialization | false | See: [Example: Explicit Initialization](http://6pac.github.com/SlickGrid/examples/example-explicit-initialization.html) |
| forceFitColumns | false | Force column sizes to fit into the container (preventing horizontal scrolling). Effectively sets column width to be 1/Number of Columns which on small containers may not be desirable |
| forceSyncScrolling | false ||
| formatterFactory | null | A factory object responsible to creating a formatter for a given cell. Must implement getFormatter(column). |
| fullWidthRows | false | Will expand the grid row div to the full width of the container, grid cell divs will remain aligned to the left (so the row div now takes in any blank space between the grid columns and the right boundary of the viewport) |
| headerRowHeight | 25 ||
| leaveSpaceForNewRows | false ||
| multiColumnSort | false | See: [Example: Multi-Column Sort](http://6pac.github.com/SlickGrid/examples/example-multi-column-sort.html) |
| multiSelect | true ||
| rowHeight|25||
| selectedCellCssClass | "selected" ||
| showHeaderRow | false||
| syncColumnCellResize | false | If true, the column being resized will change its width as the mouse is dragging the resize handle. If false, the column will resize after mouse drag ends. |
| topPanelHeight|25||





