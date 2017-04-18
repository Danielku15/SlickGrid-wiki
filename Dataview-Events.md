
| Event | Description |
|-------+-------------|
| onPagingInfoChanged | |
| onRowCountChanged | |
| onRowsChanged | |



<h3>Responding to data source changes</h3>

While this may not be immediately obvious from what you see in the examples and in the code, the key use of the grid is in MVC applications where the grid is wired to respond to events in the Model. In our application we have spreadsheet component of a Gantt chart, and the Model is a "filtered" view of the tasks (rows) in the original datasource. Suppose you collapse or expand a parent task or enter some text in a Quick Filter textbox. The Model then recalculates which rows are now visible, compares that with what was visible before and fires two events - onRowCountChanged & onRowsChanged. The latter one tells all subscribed Views, such as the grid, that the rows in specific positions changed. The grid then only has to invalidate/remove those rows and call grid.renderViewport() to make sure that whatever is in the viewport is visible. The onRowCountChanged event triggers the recalculation of the virtual canvas - grid.resizeCanvas(). Together, this pattern makes for an incredibly efficient, flexible and, most importantly, scalable implementation.

