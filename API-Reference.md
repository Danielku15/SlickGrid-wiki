NOTE:  This is a user-contributed section.

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

## Grid's Selection API

Get the list of selected grid rows:
```javascript
grid.getSelectedRows()
```

Set the rows at the following indexes as selected:
```javascript
grid.setSelectedRows([0,10])
```


## Cell API

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

   1: {
         birthday: "highlight",
         age: "highlight"
       }
})
```

`grid.addCellCssStyles(key, hash)` - The add-only sibling to `grid.setCellCssStyles(key, hash)`. Will throw an exception if you try to set the same key twice without calling `removeCellCssStyles()`. Use `setColumnCssStyles()` instead if you don't want that.

`grid.removeCellCssStyles(key)` - Removes styles under `key` from the grid.