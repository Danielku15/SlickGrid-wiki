
| Event  | Description |
|------- | ------------|
| onBeforePagingInfoChanged | Before Paging Information Changes |
| onPagingInfoChanged | Paging information has changed |
| onRowCountChanged | On total row count changed |
| onRowsChanged | On rows changed |
| onRowsOrCountChanged| On rows or count changed (combines both previous events) |

Example of handing an event:

    dataView.onRowsChanged.subscribe(function (e, args) {
      grid.invalidateRows(args.rows);
      grid.render();
    });

The events are fired in the following order.  All these events are fired by the same section of code in the ```refresh``` method of the dataView, so firing order is fixed, and information about which of the events are going to be fired is available to the firing code.

```onBeforePagingInfoChanged```  ```args: { pageSize, pageNum, totalRows, totalPages, dataView }```

```onPagingInfoChanged```  ```args: { pageSize, pageNum, totalRows, totalPages, dataView }```

(args are self explanatory - dataView is the calling dataView object)


```onRowCountChanged```  ```args: { previous, current, dataView, callingOnRowsChanged }```

- previous: previous rowcount
- current: current rowcount
- dataView: the calling dataView object
- callingOnRowsChanged: true if the ```onRowsChanged``` event is also going to be called


```onRowsChanged```  ```args: { rows, dataView, calledOnRowCountChanged}```

- rows: the rows diff (list of changed rows)
- dataView: the calling dataView object
- calledOnRowCountChanged: true if the ```onRowCountChanged``` event is also going to be called


```onRowsOrCountChanged```  ```args: { rowsDiff, previousRowCount, currentRowCount, dataView}```

- rowsDiff: the rows diff (list of changed rows)
- previousRowCount: previous rowcount
- currentRowCount: current rowcount
- dataView: the calling dataView object

This event performs the function of *both* of the other events and SHOULD BE USED INSTEAD of the other events only.


<h3>Responding to data source changes</h3>

While this may not be immediately obvious from what you see in the examples and in the code, the key use of the grid is in MVC applications where the grid is wired to respond to events in the Model.  
In our application we have spreadsheet component of a Gantt chart, and the Model is a "filtered" view of the tasks (rows) in the original datasource. Suppose you collapse or expand a parent task or enter some text in a Quick Filter textbox. The Model then recalculates which rows are now visible, compares that with what was visible before and fires two events - onRowCountChanged & onRowsChanged. 

```onRowsChanged``` tells all subscribed Views, such as the grid, that the rows in specific positions changed. The grid then only has to invalidate/remove those rows and call grid.renderViewport() to make sure that whatever is in the viewport is visible. 
```onRowCountChanged``` triggers the recalculation of the virtual canvas - grid.resizeCanvas(). Together, this pattern makes for an incredibly efficient, flexible and, most importantly, scalable implementation.

NEW EVENTS AND PARAMETERS ADDED

There has been some debate over whether two events (```onRowsChanged```, ```onRowCountChanged```) are appropriate, as 
- often both events need to do some common tasks
- each event has no way of knowing if the other event will be fired
- handling only one event often leads to hard-to-diagnose bugs 
- this situation often leads to repetition of the common tasks by both events

This is why the ```onRowsOrCountChanged``` event, rolling the two in to one, has been added.

As a workaround for the two-event scenario, additional parameters (```callingOnRowsChanged```, ```calledOnRowCountChanged```) have been added to each event to indicate whether the other event will be or has been fired, allowing the event handling code to be smarter in its responses to the events. 
