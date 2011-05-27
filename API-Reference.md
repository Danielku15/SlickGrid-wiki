## Model API:

Instead of passing SlickGrid an array of row objects, you can pass an object that holds (and updates!) all your rows. This object, which SlickGrid calls a `Model`, only needs to respond to a simple API:

```javascript
model.getItem(i) // Returns the ith row
model.getLength() // Returns the number of items
```

If you modify the nth row, you will need to tell the grid that the row is invalid, and then call `render()` to update it:

```javascript
grid.invalidateRow(n)
grid.render()
```

You can also call `grid.invalidateRows()` to invalidate a lot of rows at once, and, if you just want to re-draw the whole grid, call `grid.invalidate()` (which doesn't seem to need a `render()` call after.)
