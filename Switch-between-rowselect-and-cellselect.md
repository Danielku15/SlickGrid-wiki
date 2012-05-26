This can be used when you have checkbox selection and want to use the checkboxes for rowselection and and go back to cellselection when you click a cell. 

Make sure you have access to the `toggleRowSelection(args.row);` function

```javascript
    var rowSelect = new Slick.RowSelectionModel({selectActiveRow: true});
    var cellSelect = new Slick.CellSelectionModel();

    function handleClick(e, args) {
        //check if we just clicked a checkbox
        if (subscription.grid.getColumns()[args.cell].id === "_checkbox_selector"){
            if (grid.getSelectionModel() != rowSelect){
                grid.setSelectedRows([]);
                grid.setSelectionModel(rowSelect);
            }
            // if editing, try to commit
            if (grid.getEditorLock().isActive() && !grid.getEditorLock().commitCurrentEdit()) {
                e.preventDefault();
                e.stopImmediatePropagation();
                return;
            }
            
            toggleRowSelection(args.row);
            e.stopPropagation();
            e.stopImmediatePropagation();
        } else {
            if (subscription.grid.getSelectionModel() != cellSelect){
                subscription.grid.setSelectionModel(cellSelect);
            }
        }
    }
```