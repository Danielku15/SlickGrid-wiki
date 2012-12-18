Selecting cells in SlickGrid is handled by a *selection model*.

Selection models are controllers responsible for handling user interactions and notifying subscribers of the changes in the selection.
Selection is represented as an array of Slick.Range objects.  

You can get the current selection model from the grid by calling `getSelectionModel()` and set a different one using `setSelectionModel(selectionModel).`  By default, no selection model is set.

The grid also provides two helper methods to simplify development - getSelectedRows() and setSelectedRows(rowsArray), as well as an onSelectedRowsChanged event.

SlickGrid includes two pre-made selection models - `Slick.CellSelectionModel` and `Slick.RowSelectionModel`, but you can easily write a custom one. 

A selection model must expose:

**init**
`function init(grid)`

An initializer function that will be called with an instance of the grid whenever a selection model is registered with setSelectionModel.
The selection model can use this to initialize its state and subscribe to grid events.

**destroy**
`function destroy()`

A destructor function that will be called whenever a selection model is unregistered from the grid by a call to setSelectionModel with another selection model or whenever a grid with this selection model is destroyed.
The selection model can use this destructor to unsubscribe from grid events and release all resources (remove DOM nodes, event listeners, etc.).

**onSelectedRangesChanged**
`Slick.Event`

An event that is fired whenever the selected ranges are changed.
When a selection model is registered with the grid, the grid will subscribe to this event and use it to update the internal state and decorate selected cells with selectedCellCssClass.
The event must be fired with the following data in event args:
* _ranges_     -    An array of Slick.Range objects representing the selection.



Below is a simplistic example of a single cell selection model that only reacts to mouse clicks:

```javascript
    function SingleCellSelectionModel() {
      var self = this;

      this.init = function(grid) {
        self._grid = grid;
        self._grid.onClick.subscribe(self.handleGridClick);
      };

      this.destroy = function() {
        self._grid.onClick.unsubscribe(self.handleGridClick);
      };

      this.handleGridClick = function(e, args) {
        var cell = self._grid.getCellFromEvent(e);
        if (!cell || !self._grid.canCellBeSelected(cell.row, cell.cell)) {
          return;
        }

        self.onSelectedRangesChanged.notify([new Slick.Range(cell.row, cell.cell, cell.row, cell.cell)]);
      };
    }
```