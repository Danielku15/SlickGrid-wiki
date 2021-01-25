## Core concepts

SlickGrid is very flexible in how it consumes the data.  The data is passed to the grid via the constructor and can also be accessed using the `setData(data)` and `getData()` methods.  Data itself can be either an array-like object with a `length` property and an indexer (`data[index]`) or a custom data provider implementing the following interface:

* `getLength()` - returns the number of data items in the set
* `getItem(index)` - returns the item at a given index
* `getItemMetadata(index)` - returns the metadata for the item at a given index (optional)


DataView (`Slick.Data.DataView` included in [slick.dataview.js](../blob/master/slick.dataview.js)) is one such data provider and it is part of the SlickGrid package.
 
If all of the data is available on the client (i.e. in a JavaScript array), DataView can provide many useful features that the grid itself doesn't have. (This fact that the grid lacks these features is by design - SlickGrid tries to keep the core lean and simple while encouraging modular design and data abstraction in its API.)

DataView works by taking in your data and acting as a data provider that you pass to SlickGrid instead of your original data array. For example, if you make DataView group data, it makes the grid think that the "group" rows are just regular data items, so the grid doesn't need to be aware of them. DataView tells the grid that those items have a custom display and behavior and provides implementations of both. You then wire up DataView's `onRowCountChanged` and `onRowsChanged` events to update the grid and voila.

Here's a rough list of features that DataView adds to the grid:

* Paging.
* Multi-column sorting.
* Search.
* Multi-level grouping with totals.
* Expand/collapse groups.

DataView also enables very efficient updates in response to the changing data.  Whenever something changes, it detects which rows need updating, and passes them in the `onRowCountChanged` and `onRowsChanged` events that it fires, so instead of rerendering the entire grid, you can simply invalidate the updated rows.


## Getting started

To use the DataView, include `slick.dataview.js`:

```javascript
// Create the DataView.
var dataView = new Slick.Data.DataView();

//Create columns
var columns = [
  {id: "column1", name: "ID", field: "id"},
  {id: "column2", name: "Language", field: "lang"},
  {id: "column3", name: "Year", field: "year"}
];

// Pass it as a data provider to SlickGrid.
var grid = new Slick.Grid(containerEl, dataView, columns, options);

// Make the grid respond to DataView change events.
dataView.onRowCountChanged.subscribe(function (e, args) {
  grid.updateRowCount();
  grid.render();
});

dataView.onRowsChanged.subscribe(function (e, args) {
  grid.invalidateRows(args.rows);
  grid.render();
});
```

Now we're ready to initialize it with some data.
One important requirement that DataView imposes on the data it consumes is that every item has a unique identifier.  DataView uses it to uniquely identify items and compare them to each other.  By default, DataView uses the `id` property of the data item, but you can specify a different one by passing it in via an optional second argument in the `setItems(data, [objectIdProperty])`.  The `id` value must be serializable to a string.

```javascript
var data = [
  {'id': 'l1', 'lang': 'Java', 'year': 1995},
  {'id': 'l2', 'lang': 'JavaScript', 'year': 1995},
  {'id': 'l3', 'lang': 'C#', 'year': 2000},
  {'id': 'l4', 'lang': 'Python', 'year': 1991}];

// This will fire the change events and update the grid.
dataView.setItems(data);
```

You can call `getItems()` to get the data array back.


## Mapping rows vs items

Ok, let's reiterate - DataView takes in a data array as an input, manipulates it, and presents the results to the grid by acting as a data provider, i.e. exposing the data provider methods `getItem(index)`, `getLength()` and `getItemMetadata(index)`.  In handling grid events, it's important to always keep in mind that the row indexes the grid refers to are, in fact, the indexes into the output of the DataView!  For example, if you're handling a grid `onClick` event and it's giving you a row index, to look up the data item, you need to call `dataView.getItem(rowIndex)` and *not* `data[rowIndex]`.

In general, whenever we talk about *rows*, we mean the data as the grid sees it, so, if you're using a DataView, that would be the *output* of the DataView (`dataView.getItem(index)`).  Whenever we talk about *items*, we mean the *input* of the DataView (`data[index]` or `dataView.getItems()[index]`).  You'll notice that it is somewhat confusing that `getItem(index)` returns a *row* while `getItems()` returns *items*.  Unfortunately, it's this way for historical reasons.  `getItem(index)` is part of the  data provider interface.  In retrospect, it would be better if the DataView exposed a `getDataProvider()` method.

### DataView Methods

Since each item has a unique id, they are often used to keep track of ids/items/rows/indices and to map one to another.

These methods are exposed by the DataView as part of the data provider interface:

* `getItems()` - Returns the original data array.
* `getItem(row)` - With a row index of an item in the grid, return the item.
* `getItemMetadata(idx)` - Returns the item metadata at a given index.
* `getLength()` - Returns the number of rows in the grid.

DataView exposes several methods in order to map ids to items to rows in the grid to indices in the original data array:

* `getItemById(id)` - With an item's id, return the item.
* `getIdxById(id)` - With an item's id, return the index of the item in the original data array.
* `getRowById(id)` - With an item's id, return the row of the item in the grid.
* `getItemByIdx(idx)` - With an index of an item in the original data array, return the item. Equivalent to `getItems()[index]`.
* `mapIdsToRows(idArray)` - Maps an array of item ids into rows in the grid.
* `mapRowsToIds(rowArray)` - Maps an array of rows in the grid into item ids.

## Synchronizing selection & cell CSS styles

One of the most common questions about DataView is how to synchronize the selection or cell CSS styles state on DataView changes.  Let's say that the user selected a row.  If they then change the filter on the DataView to hide some items, the grid gets a call to invalidate all changed rows, including the selected one, but it doesn't know that the item that was displayed there has moved somewhere else.  What we need to do, is to store the ids of items that were selected, and to update the selection on the grid any time the DataView is modified.

Luckily, there is a helper method on the DataView that can take care of that:

* `syncGridSelection(grid, preserveHidden)` - Synchronizes `grid`'s selected rows with the DataView by subscribing to the grid's `onSelectedRowsChanged` event as well as the DataView's `onRowsChanged` & `onRowCountChanged` events.  If `preserveHidden` is true, it will preserve selected items even if they are not visible as rows.  For example, if you select an item, change the DataView filter so that that item is no longer presented to the grid and then change it back, the item will remain selected.  If `preserveHidden` is false, all selected items that can't be mapped onto rows are dropped.

The implementation is really simple, and I'll include it here for the reference:

```javascript
function syncGridSelection(grid, preserveHidden) {
  var self = this;
  var selectedRowIds = self.mapRowsToIds(grid.getSelectedRows());;
  var inHandler;

  function update() {
    if (selectedRowIds.length > 0) {
      inHandler = true;
      var selectedRows = self.mapIdsToRows(selectedRowIds);
      if (!preserveHidden) {
        selectedRowIds = self.mapRowsToIds(selectedRows);
      }
      grid.setSelectedRows(selectedRows);
      inHandler = false;
    }
  }

  grid.onSelectedRowsChanged.subscribe(function(e, args) {
    if (inHandler) { return; }
    selectedRowIds = self.mapRowsToIds(grid.getSelectedRows());
  });

  this.onRowsChanged.subscribe(update);

  this.onRowCountChanged.subscribe(update);
}
```

**NOTE:**  This only works with the RowSelectionModel.  CellSelectionModel isn't supported yet (I'm open to pull requests!).


There is a similar helper method to synchronize the cell CSS styles:

```javascript
function syncGridCellCssStyles(grid, key) {
  var hashById;
  var inHandler;

  // since this method can be called after the cell styles have been set,
  // get the existing ones right away
  storeCellCssStyles(grid.getCellCssStyles(key));

  function storeCellCssStyles(hash) {
    hashById = {};
    for (var row in hash) {
      var id = rows[row][idProperty];
      hashById[id] = hash[row];
    }
  }

  function update() {
    if (hashById) {
      inHandler = true;
      ensureRowsByIdCache();
      var newHash = {};
      for (var id in hashById) {
        var row = rowsById[id];
        if (row != undefined) {
          newHash[row] = hashById[id];
        }
      }
      grid.setCellCssStyles(key, newHash);
      inHandler = false;
    }
  }

  grid.onCellCssStylesChanged.subscribe(function(e, args) {
    if (inHandler) { return; }
    if (key != args.key) { return; }
    if (args.hash) {
      storeCellCssStyles(args.hash);
    }
  });

  this.onRowsChanged.subscribe(update);

  this.onRowCountChanged.subscribe(update);
}
```



## Sorting

Sorting is pretty simple:

```javascript
// Subscribe to the grid's onSort event.
// It only gets fired for sortable columns, so make sure your column definition has `sortable = true`.
grid.onSort.subscribe(function(e, args) {
  // args.multiColumnSort indicates whether or not this is a multi-column sort.
  // If it is, args.sortCols will have an array of {sortCol:..., sortAsc:...} objects.
  // If not, the sort column and direction will be in args.sortCol & args.sortAsc.

  // We'll use a simple comparer function here.
  var comparer = function(a, b) {
    return (a[args.sortCol.field] > b[args.sortCol.field]) ? 1 : -1;
  }

  // Delegate the sorting to DataView.
  // This will fire the change events and update the grid.
  dataView.sort(comparer, args.sortAsc);
});
```

Note that calling `sort()` on the DataView modifies the original `data` array that was passed in to `setItems(data)`!

There's also a `fastSort(field, isAscending)` method on the DataView to do a fast lexicographic search that is especially handy for older versions of IE.


## Updating data

Since DataView can't automatically detect when you're changing the data, you'll need to make these updates via the DataView.  These updates will be applied directly to the original `data` array.

```javascript
// Delete item with id 'l3' ('C#').
dataView.deleteItem('l3');

// Append item to the end.
dataView.addItem({'id': 'l5', 'lang': 'CoffeeScript'});

// Insert item at the beginning.
dataView.insertItem(0, {'id': 'l6', 'lang': 'TypeScript'});

// Update an existing item.
var item = dataView.getItemById('l4');
item['lang'] = 'Clojure';
dataView.updateItem('l4', item);
```

Each one of these updates will fire change events and the grid will get updated automatically.

If you have multiple items to be added, edited or deleted there are also dedicated update methods for that: 
```javascript
// Delete item with id 'l3' ('C#') and 'l4' ('Java').
dataView.deleteItems(['l3', 'l4']);

// Append items to the end.
dataView.addItems([
    {'id': 'l5', 'lang': 'CoffeeScript'},
    {'id': 'l6', 'lang': 'TypeScript'}
]);

// Insert items at the beginning.
dataView.insertItems(0, [
    {'id': 'l7', 'lang': 'Go'},
    {'id': 'l8', 'lang': 'Ruby'},
]);

// Update  existing item.
dataView.updateItems(
    ['l7', 'l8'],
    [
        {'id': 'l9', 'lang': 'C'},
        {'id': 'l10', 'lang': 'C++'},        
    ]
);
```

## Batching updates

Notice that in the example above, each update will result in the DataView recalculating its data and firing change events, resulting in the grid rerendering affected rows.  If you need to make multiple changes, you should batch them up to avoid unnecessary operations:

```javascript
// Suspend recalculations until endUpdate() is called.
dataView.beginUpdate();

dataView.addItem(...);
dataView.addItem(...);
dataView.sort(...);

// Indicate that we're done updating.
dataView.endUpdate();
```

The DataView also support "bulk" update operations optimizing the operations even further by delaying certain operations
to the `endUpdate` call. These bulk dates and more efficient operations come at cost of inconsistencies when accessing
data while updating. It is recommended to only use this bulk update in case of clear update operations where data
access to the intermediate updated state is not required. Another important part is to avoid inserting items with ids
that have been marked for deletion.

```javascript
dataView.beginUpdate(true /* activates the bulk operations */);
dataView.deleteItems(['l1', 'l2', 'l3']);
dataView.addItems([
    { 'id': 'l20', 'lang': 'Kotlin' },
    { 'id': 'l21', 'lang': 'Swift' },
    { 'id': 'l22', 'lang': 'Objective-C' }
    // many more..
]);
dataView.insertItems(0, [
    { 'id': 'l100', 'lang': 'Dart' },
    { 'id': 'l101', 'lang': 'F#' },
    { 'id': 'l102', 'lang': 'Fortran' }
]);
dataView.endUpdate();
```

## Filtering

You can customize filtering on the DataView by using dataView.setFilter(someFunction). Here's an example of a custom filter that does a case-insensitive search of all the column fields based on an input text element:

```
dataView.setFilter(searchFilter);

$('#textsearch').on('input', function () {
    dataView.setFilterArgs({ searchString: $(this).val() });
    dataView.refresh();
});

function searchFilter(item, args) {
    if (_.get(args, 'searchString.length')) {
        const values = Object.values(item);
        let isMatch = false;
        for (i = 0; i < values.length; i++) {
            if (values[i] && values[i].toString().toLowerCase().indexOf(args.searchString.toLowerCase()) >= 0) {
                isMatch = true;
                break;
            }
        }
        return isMatch;
    }
    return true;
}
```


## Paging

## Grouping

Use the GroupItemMetadataProvider plugin found in 'slick.groupitemmetadataprovider.js' and call dataView.setGrouping(groupingDef), as shown here:

```
const groupItemMetadataProvider = new Slick.Data.GroupItemMetadataProvider();

const dataView = new Slick.Data.DataView({
    groupItemMetadataProvider: groupItemMetadataProvider,
    inlineFilters: true
});

const groupingDef = {
    getter: "duration",
    formatter: function (g) {
        return "Duration:  " + g.value + "  <span style='color:green'>(" + g.count + " items)</span>";
    },
    comparer: function (a, b) {
        return a.count - b.count;
    },
    aggregators: [
        new Slick.Data.Aggregators.Avg("percentComplete"),
        new Slick.Data.Aggregators.Sum("cost"),
        new Slick.Data.Aggregators.Count("cost")
    ],
    aggregateCollapsed: aggregateCollapsed,
    lazyTotalsCalculation: true
}

dataView.setGrouping(groupingDef);

self.grid.registerPlugin(groupItemMetadataProvider);
```

You can define custom aggregators like this:

```
...
aggregators: [ new CustomAggregator('cost') ],
...
function CustomAggregator(field) {
    this.field_ = field;

    this.init = function () {
        this.sum_ = null;
    };

    //accumulate iterates over the rows. If you do not define accumulate, then it will not iterate.
    this.accumulate = function (item) {
        var val = item[this.field_];
        if (val != null && val !== "" && !isNaN(val)) {
            this.sum_ += parseFloat(val);
        }
    };

    this.storeResult = function (groupTotals) {
        if (!groupTotals.sum) {
            groupTotals.sum = {};
        }
        groupTotals.sum[this.field_] = this.sum_;
    }
}
```

## Advanced topics

## API reference
