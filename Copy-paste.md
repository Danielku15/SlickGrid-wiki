First we create an invisible textfield

```javascript
var gridPlaceHolder = '#myPlaceHolder';
$(gridPlaceHolder).append('<div style="position:absolute;top:0;left:-200;"><textarea id="' + gridPlaceHolder.substring(1) + '-cp" type="text" ></textarea></div>');
```


Now our keydown implementation
```javascript
    grid.onKeyDown.subscribe(handleKeyDown);

    function handleKeyDown(e, args) {
        function nvl(val){
            if(val){
                return val;
            }
            return "";
        }
        var cp = gridPlaceHolder + '-cp';
        if (grid.getEditorLock().isActive()) { return; }
        if (!(e.ctrlKey || e.metaKey)) { return; }
        //copy
        if (e.which == 67){
            var range = grid.getSelectionModel().getSelectedRanges()[0];
            var val = "";
            var columns = grid.getColumns();
            var h = range.toRow - range.fromRow;
            var w = range.toCell - range.fromCell;
            for (var i = 0; i <= h; i++) {
                for (var j = 0; j <= w; j++) {
                    val += nvl(data[range.fromRow + i][columns[range.fromCell + j].field]);
                    if (j < w){
                        val += "\t";
                    }
                }
                if(i < h){
                    val += "\r\n";
                }
            }
            $(cp).val(val);
            $(cp).focus();
            $(cp).select();
            e.srcElement.focus();
        } else if (e.which == 86) {
            //paste
            $(cp).focus();
            $(cp).select();
            setTimeout(function(){
                var val = $(cp).val().replace(/\r/g,"");
                var newData = val.split('\n');
                for (var i = 0; i <newData.length; i++){
                    newData[i] = newData[i].split('\t');
                }
                var range = grid.getSelectionModel().getSelectedRanges()[0];
                var columns = grid.getColumns();
                var h = range.toRow - range.fromRow;
                var w = range.toCell - range.fromCell;
                for (var i = 0; i <= h; i++) {
                    for (var j = 0; j <= w; j++) {
                        data[range.fromRow + i][columns[range.fromCell + j].field] = newData[i][j];                                
                    }
                }
                grid.invalidate();
                grid.render();
            }, 10);
            e.srcElement.focus();
            return false;
        } else if (e.which == 88){
            //cut
            var range = grid.getSelectionModel().getSelectedRanges()[0];
            var val = "";
            var columns = grid.getColumns();
            var h = range.toRow - range.fromRow;
            var w = range.toCell - range.fromCell;
            for (var i = 0; i <= h; i++) {
                for (var j = 0; j <= w; j++) {
                    val += nvl(data[range.fromRow + i][columns[range.fromCell + j].field]);
                    data[range.fromRow + i][columns[range.fromCell + j].field] = undefined;
                    if (j < w){
                        val += "\t";
                    }
                }
                if(i < h){
                    val += "\r\n";
                }
            }
            grid.invalidate();
            grid.render();
            $(cp).val(val);
            $(cp).focus();
            $(cp).select();
            e.srcElement.focus();
        }
    }
```
