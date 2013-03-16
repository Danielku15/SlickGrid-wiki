## Core concepts

SlickGrid is very flexible in how it consumes the data.  The data is passed to the grid via the constructor and can also be accessed using the `setData(data)` and `getData()` methods.  Data itself can be either an array-like object with a `length` property and an indexer (`data[index]`) or a custom data provider implementing the following interface:

* `getLength()` - returns the number of data items in the set
* `getItem(index)` - returns the item at a given index
* `getItemMetadata(index)` - returns the metadata for the item at a given index (optional)


DataView (`Slick.Data.DataView` included in `slick.dataview.js`) is one such data provider and it is part of the SlickGrid package.
 
If all of the data is available on the client (i.e. in a JavaScript array), DataView can provide many useful features that the grid itself doesn't have. (This fact that the grid lacks these features is by design - SlickGrid tries to keep the core lean and simple while encouraging modular design and data abstraction in its API.)

DataView works by taking in your data and acting as a data provider that you pass to SlickGrid instead of your original data array. For example, if you make DataView group data, it makes the grid think that the "group" rows are just regular data items, so the grid doesn't need to be aware of them. DataView tells the grid that those items have a custom display and behavior and provides implementations of both. You then wire up DataView's `onRowCountChanged` and `onRowsChanged` events to update the grid and voila.

Here's a rough list of features that DataView adds to the grid:

* Paging.
* Mutli-column sorting.
* Search.
* Multi-level grouping with totals.
* Expand/collapse groups.

DataView also enables very efficient updates in response to the changing data.  Whenever something changes, it detects which rows need updating, and passes them in the 'onRowCountChanged` and `onRowsChanged` events that it fires, so instead of rerendering the entire grid, you can simply invalidate the updated rows.


## Getting started

To use the DataView, include `slick.dataview.js`:

```javascript
// Create the DataView.
var dataView = new Slick.Data.DataView();

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
One important requirement that DataView imposes on the data it consumes is that every item has a unique identifier.  DataView uses it to uniquely identify items and compare them to each other.  By default, DataView uses the `id` property of the data item, but you can specify a different one by passing it in via an optional second argument in the `setData(data, [objectIdProperty])`.  The `id` value must be serializable to a string.

```javascript
var data = [
  {'id': 'l1', 'lang': 'Java'},
  {'id': 'l2', 'lang': 'JavaScript'},
  {'id': 'l3', 'lang': 'C#'},
  {'id': 'l4', 'lang': 'Python'}];

// This will fire the change events and update the grid.
dataView.setItems(data);
```

You can call `getItems()` to get the data array back.


## Mapping rows vs items



 




## Sorting

Sorting is pretty simple:

```javascript
// Subscribe to the grid's onSort event.
// It only gets fired for sortable columns, so make sure your column definition has `sortable = true`.
grid.onSort.subscribe(function(e, args) {
  // We'll use a simple comparer function here.
  var comparer = function(a, b) {
    return a[args.sortCol] > b[args.sortCol];
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


## Batching updates

Notice that in the example above, each update will result in the DataView recalculating its data and firing change events, resulting in the grid rerendering affected rows.  If you need to make multiple changes, you should batch them up to avoid unnecessary operations:

```javascript
// Suspend recalculations until endUpdate() is called.
dataView.startUpdate();

dataView.addItem(...);
dataView.addItem(...);
dataView.sort(...);

// Indicate that we're done updating.
dataView.endUpdate();
```


## Filtering




## Paging

## Grouping

## Advanced topics

## API reference

