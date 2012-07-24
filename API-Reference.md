# NOTE:  This is a user-contributed section, so it may not be accurate!!!


## Model API:

Instead of passing SlickGrid an array of row objects, you can pass an object that holds (and updates!) all your rows. This object, which SlickGrid calls a `Model`, only needs to respond to a simple API:

```javascript
model.getItem(i) // Returns the ith row
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
Column options:


**Booleans**


##
* sortable
* resizable
* rerenderOnResize
* focusable
* selectable


**Other**

##
* id _A unique identifier for the column within the grid_
* name _The display text_
* field _The name of the data object property to pull content from_
* editor _The editor for cell edits {TextEditor, IntegerEditor, DateEditor...} See slick.editors.js
* cssClass 
* headerCssClass
* width
* minWidth
* maxWidth
* toolTip

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



## cellEditor API

`cellEditor.applyValue(item, state)` - 

`cellEditor.destroy()` - 

`cellEditor.focus(input)` - 

`cellEditor.isValueChanged()` - 

`cellEditor.loadValue(item)` - 

`cellEditor.serializeValue()` - 

`cellEditor.validate()` - 

## Custom Field Accessor
By default field values are access via `item[columnDef.field]`. To have a custom field accessor, overwrite the default `dataItemColumnValueExtractor` option.

```
  var options = {
	dataItemColumnValueExtractor: function(item, colDef) {
	  return item.get(colDef.id);
	}
  };
```