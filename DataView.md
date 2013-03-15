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
var dataView = new Slick.Data.DataView();

```


## Updating data

## Batching updates

## Sorting

## Filtering

## Paging

## Grouping


## API reference



