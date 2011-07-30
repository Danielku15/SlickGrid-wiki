The following is an incomplete list of column options:  

id : object  
    An object that can be used to identify this row.  
name : string  
    The name that will be used for the column header, and lookups.  

field : string  
    The property of each data item that will be used to supply the grid with data.  

formatter : function  
    A function that accepts the data item and returns an HTML string:  
<pre>
    function(row,cell,value,columnDef,dataContext){
         return value.anInterestingProperty;
    }
</pre>

editor: function  
    A function that accepts args and returns an object with a set of required functions. (See 'writing custom editors'):https://github.com/mleibman/SlickGrid/wiki/Writing-custom-cell-editors  

width : integer  
    Absolute width when the grid has forceFill set to false, effectively relative width when forceFill is true.  

sortable : bool  
  Indicates that SlickGrid should fire sort events when the column header is clicked for this column.  