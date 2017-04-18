## Basic interface

    function IEditor(args) {

        // initialize the UI


        /*********** REQUIRED METHODS ***********/

        this.destroy = function() {
            // remove all data, events & dom elements created in the constructor
        };

        this.focus = function() {
            // set the focus on the main input control (if any)
        };

        this.isValueChanged = function() {
            // return true if the value(s) being edited by the user has/have been changed
            return false;
        };

        this.serializeValue = function() {
            // return the value(s) being edited by the user in a serialized form
            // can be an arbitrary object
            // the only restriction is that it must be a simple object that can be passed around even
            // when the editor itself has been destroyed
            return "";
        };

        this.loadValue = function(item) {
            // load the value(s) from the data item and update the UI
            // this method will be called immediately after the editor is initialized
            // it may also be called by the grid if if the row/cell being edited is updated via grid.updateRow/updateCell
        };

        this.applyValue = function(item,state) {
            // deserialize the value(s) saved to "state" and apply them to the data item
            // this method may get called after the editor itself has been destroyed
            // treat it as an equivalent of a Java/C# "static" method - no instance variables should be accessed
        };

        this.validate = function() {
            // validate user input and return the result along with the validation message, if any
            // if the input is valid, return {valid:true,msg:null}
            return { valid: false, msg: "This field is required" };        
        };


        /*********** OPTIONAL METHODS***********/

        this.hide = function() {
            // if implemented, this will be called if the cell being edited is scrolled out of the view
            // implement this is your UI is not appended to the cell itself or if you open any secondary
            // selector controls (like a calendar for a datepicker input)
        };

        this.show = function() {
            // pretty much the opposite of hide
        };

        this.position = function(cellBox) {
            // if implemented, this will be called by the grid if any of the cell containers are scrolled
            // and the absolute position of the edited cell is changed
            // if your UI is constructed as a child of document BODY, implement this to update the
            // position of the elements as the position of the cell changes
            // 
            // the cellBox: { top, left, bottom, right, width, height, visible }
        };
    }


### Constructor arguments
The editor constructor receives an `args` object which has the following fields:
* `column` &mdash; column definition object
* `container` &mdash; DOM-object for cell container
* `grid` &mdash; grid instance
* `gridPosition` &mdash; object describing grid position 
* `item` &mdash; data item for edited row
* `position` &mdash; object describing cell position 
* `cancelChanges()` &mdash; grid method to discard changes
* `commitChanges()` &mdash; grid method to store changes

## Compound editors
In most cases, there will be a one-to-one relationship between the fields of your data objects and cells in the grid.
Occasionally, though, you may want to combine several fields into one cell in order to improve the usability of your application.  A custom formatter can easily pull information from multiple fields of your data object and present it in one cell.  SlickGrid handles edition those cells by using the `loadValue()`, `serializeValue()` and `applyValue()` methods of your editor.  While it may seem more complicated than a simple `getValue()` and `setValue()`, without them, compound editors would not have been possible.

A sample compound editor is implemented in example 3a ([source](http://github.com/6pac/SlickGrid/blob/master/examples/example3a-compound-editors.html), [demo](http://6pac.github.com/SlickGrid/examples/example3a-compound-editors.html)).

## Intercepting cell edits
You can easily use the `onCellChange` event to run some code after the cell has been edited.  You can also intercept all cell edits and have complete control over how and when those edits are committed by specifying a custom handler by setting the `editCommandHandler` grid option.  Due to the disconnected nature of `applyValue()` and `serializeValue()`, you can even undo your changes after you commit them.  This can be especially handy if you are editing a remote data source - you can apply the changes and make an AJAX call passing the undo callback as the error handler, so that your data doesn't get out of sync if the server cannot save the values.  You can also queue up the edit commands and implement undo/redo functionality in just a few lines of code.

The `editCommandHandler` is called right after the editor's `destroy()` method has been called, and is passed the item being edited, the column definition, and the edit command:
<pre>function editCommandHandler(item,column,editCommand) {}</pre>

The `editCommand` consists of:
<li>`row`:  the row of the cell being edited
<li>`cell`:  the column of the cell being edited
<li>`editor`:  a reference to the cell editor
<li>`serializedValue`:  serialized value; the result of calling editor.serializeValue() right before destroying the editor
<li>`prevSerializedValue`:  the result of calling editor.serializeValue() before the changes have been made by the user
<li>`execute()`:  a callback to apply the changes using editor.applyValue(item,serializedValue) and update the row
<li>`undo()`:  a callback to undo the changes using editor.applyValue(item,prevSerializedValue) and update the row

A sample spreadsheet with undo is implemented in the example 3b ([source](http://github.com/6pac/SlickGrid/blob/master/examples/example3b-editing-with-undo.html, "demo](http://6pac.github.com/SlickGrid/examples/example3b-editing-with-undo.html)).
