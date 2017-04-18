Although the source of the [first example](http://6pac.github.com/SlickGrid/examples/example1-simple.html) is self-explanatory, it's worth pointing out the basics of SlickGrid. The following line:

`var slickgrid = new Slick.Grid(container, rows, columns, options);`

initializes and renders SlickGrid, and assigns its interface to the `slickgrid` var. Now we can use `slickgrid.someMethod()` in order to interact with it.

**Container**

`container` (an Element or a jQuery selector) points to the HTML element where the grid will be created, typically being an empty `<div>`. The `<div>` should have explicit dimensions (height and width) specified via CSS or the `style` attribute. The grid will be sized to occupy all available space.

**Rows**

`rows` is an array of data objects. Example:

    var rows = [
        {
            field_1: "value1",
            field_2: "value2"
        }, {
            field_1: "value3",
            field_2: "value4"
        }
    ];

Providing data to the grid is explained in more detail [here](https://github.com/6pac/SlickGrid/wiki/Providing-data-to-the-grid).

As it is passed by reference to the grid, you can modify it directly, but since the grid doesn't know when the data has changed, you need to let it know that it needs to rerender:

    slickgrid.invalidate();

This forces all the rows to be destroyed and recreated, but since the grid only renders the rows in the viewport (plus a small buffer), the performance of this method is constant and does not depend on the number of rows in the dataset. If you want to be more efficient, however, you can let the grid know exactly which rows need to be rerendered and whether the number of rows has changed:

    slickgrid.invalidateRows([4, 7]);
    slickgrid.updateRowCount();
    slickgrid.render();

Doing that will make the grid rerender rows 4 and 7 (0-based) as well as update the number of rows (new rows will be rendered and rows no longer in the dataset will be removed).

This is one of key strengths of SlickGrid which allows for extremely efficient UI updates.

**Columns**

`columns` is an array of objects, having at least the following fields:

* _name_ - The name to be displayed in the view.
* _field_ - The field name used in the data row objects.
* _id_ - An unique identifier for each column in the model, allowing to set more than one column reading the same field.

Other fields include:

        resizable
        sortable
        selectable
        focusable
        width
        minWidth
        maxWidth
        rerenderOnResize
        headerCssClass
        formatter
        editor
        etc.

Example:

    var columns = [
        {
            name: "Address",
            field: "address",
            id: "address",  // In most cases field and id will have the same value.
            sortable: true
        }, 
        {
            name: "Rating, in %",
            field: "rating", // This and the following column read the same data, but can present it in a different way.
            id: "rating_percent",
            resizable: false
        }, 
        {
            name: "Rating, in stars",
            field: "rating",
            id: "rating_stars"
        }
    ];

**Options**

`options` allows you to specify [additional options](https://github.com/6pac/SlickGrid/wiki/Grid-Options).

**Events**

SlickGrid has its own simple implementation of events.  To subscribe to an event, call `event.subscribe()` and pass in a function that will take two parameters - an `event` object that contains the browser event, if any, and an additional `args` object that contains data passed from the grid.

An example:

    slickgrid.onDblClick.subscribe(function(e, args){
        var args.item; // object containing name, field, id, etc
    });

See the [events](https://github.com/6pac/SlickGrid/wiki/Grid-Events) for the full list.

**Basic sorting**

It can be achieved by listening the `onSort` method:

		slickgrid.onSort.subscribe(function(e, args){ // args: sort information. 
			var field = args.sortCol.field;
			
			rows.sort(function(a, b){
				var result = 
					a[field] > b[field] ? 1 :
					a[field] < b[field] ? -1 :
					0;
					
				return args.sortAsc ? result : -result;
			});
			
			slickgrid.invalidate();			
		});