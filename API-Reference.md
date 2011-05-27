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

You can also call `grid.invalidateRows()` to invalidate a lot of rows at once, and, if you just want to re-draw the whole grid, call `grid.invalidate()` (which doesn't seem to need a `render()` call after.)


`grid.scrollRowIntoView(rowIndex)` - scroll the grid until a row is visible.
```javascript
grid.scrollRowIntoView(100)
```

## Column API

`grid.getColumnIndex(columnName)` - Returns the numeric index of the given column. Useful when a column index is required by the API.

```javascript
grid.getColumnIndex('first_name')
```

## Cell API

`grid.setColumnCssStyles(key, hash)` - Sets CSS classes to specific grid cells. `key` is a sort of cache key that names your set of styles and ensures you don't apply the same change twice.

```css
   .highlight{ background: yellow } 
```

```javascript
grid.setColumnCssStyles("birthday_highlight", {
   0: {
        birthday: "highlight", 
        age: "highlight"
       },

   1: {
         birthday: "highlight",
         age: "highlight"
       }
}
```