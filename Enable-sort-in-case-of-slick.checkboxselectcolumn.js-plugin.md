This behavior can be achieved by the in the following modifications:
* Declare a slick event such as onRenderCompleted in slick.grid.js which will assure grid rendering completed.
* Preserving present row_ids while clicking on the check boxes.
* After sorting operation completed [ e.g onRenderCompleted  ] successfully, searching for present position of  preserved row_ids by iterating the grid rows.
* Update selected rows with the present position found in the previous step.

**Detail Approach**

Declare a slick event such as onRenderCompleted in slick.grid.js which will assure grid rendering completed. To support this feature it will be required to do trigger an action when render() method has completed its task hence need to add the following line to the render() method just below renderRows(rendered);

`[slick.grid.js]     
 
      //Add a new event handler to the public API:
      "onRenderCompleted": new Slick.Event(),
      //Add the following line to the render() method just below renderRows(rendered);
      function render() {
        ...
        renderRows(rendered);
        trigger(self.onRenderCompleted, {}); // fire when rendering is done
        ...
      }`

Preserving present row_ids while clicking on the check boxes. In igv.slick.checkboxselectcolumn.js , handleClick API gets triggered onClick operation on the grid and inside handleClick API preserving present row_ids operation gets executed if and only if clicking on a row select check-box. Refer to the following code snippets which will elaborate the code life cycle.

`[slick.checkboxselectcolumn.js]     


      function CheckboxSelectColumn(options) {
      // Introducing new variables
      var preserveSelectedRow = [];
      var preserveSelectedRowID = [];
  
      // Existing Code
      function init(grid) {
           _grid = grid;
           _grid.onClick.subscribe(handleClick);
       }
   
      // preserving present row_ids operation gets executed if and only if clicking on a row select checkbox
      function handleClick(e, args) {
       if(_grid.getColumns()[args.cell].id === _options.columnId && $(e.target).is(":checkbox")) {
           Var i;
           // Preserving Selected Rows
           preserveSelectedRow = _grid.getSelectedRows();
           // Preserving Selected Row ID
           preserveSelectedRowID = [];
           for (i = 0; i < preserveSelectedRow.length; i++) {
               preserveSelectedRowID.push(_grid.getDataItem(preserveSelectedRow[i]).id);
           }
       }
      }
    }`

After sorting operation is completed [ e.g onRenderCompleted  ] successfully, search for present position of preserved row_ids by iterating the grid rows and then update selected rows with the present position found. Refer to the following code snippets which will elaborate the code life cycle.

`[slick.checkboxselectcolumn.js]      


       function CheckboxSelectColumn(options) {
        // Existing Code
        function init(grid) {
            _grid = grid;
            // Subscribing handleSort API which will be
            // triggered on onSort operation of grid column
            _grid.onSort.subscribe(handleSort);
        }
    
        var handleSort = function (e, args){
          // Subscribing handleCheckBox API which will be
          // triggered when rendering operation of grid is completed
          // after sorting.
          args.grid.onRenderCompleted.subscribe(handleCheckBox);
        }
 
        var handleCheckBox = function (e, args){
           var grid = args.grid;
           var selectedRows = grid.getSelectedRows();
           var newPosition = [];
           var position, i, j;
           // Iterating all rows of the grid and found the
           // position of the previously selected [ Before Sort ]
           // items.
           for (i = 0; i < selectedRows.length; i++) {
                position = -1;
                for (j = 0; j < grid.getData().getItems().length; j++) {
                   position = $.inArray( grid.getDataItem(j).id, preserveSelectedRowID );
                   if(position >= 0){
                      // Items found and inserting the postion into
                      // newPosition Array
                      newPosition.push(j);
                   }
                }  
           }
           // If newPosition is not empty then
           // re-ordering the selection as per new position.
           if(newPosition.length > 0){
              grid.onRenderCompleted.unsubscribe(handleCheckBox);
              grid.setSelectedRows(newPosition);
           }
           grid.onRenderCompleted.unsubscribe(handleCheckBox);
       }
     
     }
`