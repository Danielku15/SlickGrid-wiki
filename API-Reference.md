## NOTE:  This is a user-contributed section, so it may not be accurate!!!


## Data Provider API:

Instead of passing SlickGrid an array of row objects, you can pass an object that holds (and updates!) all your rows. This object, which SlickGrid calls a `data provider`, only needs to respond to a simple API:

```javascript
model.getItem(i) // Returns the ith row
model.getItemMetadata(i) // Returns the column metadata for the ith row or null if none is available.
model.getLength() // Returns the number of items
```

## Row API

If you modify the nth row, you will need to tell the grid that the row is invalid, and then call `render()` to update it:

```javascript
grid.invalidateRow(n)
grid.render()
```

You can also call `grid.invalidateRows()` to invalidate a lot of rows at once, and, if you just want to re-draw the whole grid, call `grid.invalidate()` (which would do a `render()` automatically.)


`grid.scrollRowIntoView(rowIndex)` - scroll the grid until a row is visible.
```javascript
grid.scrollRowIntoView(100)
```

## Column API

`grid.getColumnIndex(columnName)` - Returns the numeric index of the given column. Useful when a column index is required by the API.

```javascript
grid.getColumnIndex('first_name')
```

When you initialize SlickGrid, you can pass it an array of column options, one for each column. These options allow you to customize the grid's look and behavior on a column-by-column basis. For example:

```javascript
var columns = [
  {id: "userId", name: "id", field: "userId"},
  {id: "userName", name: "Name", field: "userName", sortable: false},
  {id: "favorites", name: "Favorites", field: "favorites", cssClass: "myCustomFavoritesStyling"}
];

// ... continue with SlickGrid setup ...

grid = new Slick.Grid("#myGrid", dataView, columns, options);

```

* **[Complete list of annotated column options](https://github.com/mleibman/SlickGrid/wiki/Column-Options)**

## Grid's Selection API

Get the list of selected grid rows:
```javascript
grid.getSelectedRows() // returns [0,1] if the first two rows are selected.
```

Set the rows at the following indexes as selected:
```javascript
grid.setSelectedRows([0,10])
```


## Cell API

`grid.addCellCssStyles(key, hash)` - The add-only sibling to `grid.setCellCssStyles(key, hash)`. Will throw an exception if you try to set the same key twice without calling `removeCellCssStyles()`. Use `setColumnCssStyles()` instead if you don't want that.

`grid.canCellBeActive(row, cell)` - returns a boolean.

`grid.canCellBeSelected(row, cell)` - returns a boolean.
 
`grid.editActiveCell(editor)` - 

`grid.flashCell(row, cell, speed)` - flashes the cell twice by toggling the CSS class 4 times. Waits _speed_ ms between toggles.

`grid.getActiveCell()` - gets an object representing the coordinates of the currently active cell {row: activeRow, cell: activeCell}

`grid.getActiveCellPosition()` - 

`grid.getCellEditor()` - gets the cell editor for the currently active cell.

`grid.removeCellCssStyles(key)` - Removes styles under `key` from the grid.

`grid.resetActiveCell()` -

`grid.setActiveCell(row, cell)` -

`grid.setCellCssStyles(key, hash)` - Sets CSS classes to specific grid cells. `key` is name for this set of styles so you can reference it later - to modify it or remove it, for example. `hash` is a per-row-index, per-column-name nested hash of CSS classes to apply.

Since all that sounds complicated, and `mleibman` can probably explain it better, here is an example.
Suppose you have a grid with columns:

["login", "name", "birthday", "age", "likes_icecream", "favorite_cake"]

...and you'd like to highlight the "birthday" and "age" columns for people whose birthday is today, in this case, rows at index 0 and 9. (The first and tenth row in the grid).

```css
   .highlight{ background: yellow } 
```

```javascript
grid.setCellCssStyles("birthday_highlight", {
   0: {
        birthday: "highlight", 
        age: "highlight" 
       },

   9: {
         birthday: "highlight",
         age: "highlight"
       }
})
```

`grid.updateCell(row, cell)` -


## Custom Field Accessor
By default field values are accessed via `item[columnDef.field]`. To have a custom field accessor, overwrite the default `dataItemColumnValueExtractor` option.

```
  var options = {
	dataItemColumnValueExtractor: function(item, colDef) {
	  return item.get(colDef.id);
	}
  };
```