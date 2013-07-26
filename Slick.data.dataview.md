

    Explore
    Gist
    Blog
    Help

    madhu7

    224
    3,274
    789

public mleibman/SlickGrid

SlickGrid / examples / example-grouping.html
mleibman 4 months ago
Upgraded to drag/drop 2.2 and fixed a bugfix lost in the gh-pages cle…

1 contributor
file 392 lines (346 sloc) 12.68 kb
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291 292 293 294 295 296 297 298 299 300 301 302 303 304 305 306 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381 382 383 384 385 386 387 388 389 390 391 	

<!DOCTYPE HTML>
<html>
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1">
  <title>SlickGrid example: Grouping</title>
  <link rel="stylesheet" href="../slick.grid.css" type="text/css"/>
  <link rel="stylesheet" href="../controls/slick.pager.css" type="text/css"/>
  <link rel="stylesheet" href="../css/smoothness/jquery-ui-1.8.16.custom.css" type="text/css"/>
  <link rel="stylesheet" href="examples.css" type="text/css"/>
  <link rel="stylesheet" href="../controls/slick.columnpicker.css" type="text/css"/>
  <style>
    .cell-effort-driven {
      text-align: center;
    }

    .slick-group-title[level='0'] {
      font-weight: bold;
    }

    .slick-group-title[level='1'] {
      text-decoration: underline;
    }

    .slick-group-title[level='2'] {
      font-style: italic;
    }
  </style>
</head>
<body>
<div style="position:relative">
  <div style="width:600px;">
    <div class="grid-header" style="width:100%">
      <label>SlickGrid</label>
    </div>
    <div id="myGrid" style="width:100%;height:500px;"></div>
    <div id="pager" style="width:100%;height:20px;"></div>
  </div>

  <div class="options-panel" style="width:450px;">
    <b>Options:</b>
    <hr/>
    <div style="padding:6px;">
      <label style="width:200px;float:left">Show tasks with % at least: </label>

      <div style="padding:2px;">
        <div style="width:100px;display:inline-block;" id="pcSlider"></div>
      </div>
      <br/><br/>
      <button onclick="loadData(50)">50 rows</button>
      <button onclick="loadData(50000)">50k rows</button>
      <button onclick="loadData(500000)">500k rows</button>
      <hr/>
      <button onclick="dataView.setGrouping([])">Clear grouping</button>
      <br/>
      <button onclick="groupByDuration()">Group by duration & sort groups by value</button>
      <br/>
      <button onclick="groupByDurationOrderByCount(false)">Group by duration & sort groups by count</button>
      <br/>
      <button onclick="groupByDurationOrderByCount(true)">Group by duration & sort groups by count, aggregate
        collapsed
      </button>
      <br/>
      <br/>
      <button onclick="groupByDurationEffortDriven()">Group by duration then effort-driven</button>
      <br/>
      <button onclick="groupByDurationEffortDrivenPercent()">Group by duration then effort-driven then percent.</button>
      <br/>
      <br/>
      <button onclick="dataView.collapseAllGroups()">Collapse all groups</button>
      <br/>
      <button onclick="dataView.expandAllGroups()">Expand all groups</button>
      <br/>
    </div>
    <hr/>
    <h2>Demonstrates:</h2>
    <ul>
      <li>
        Fully dynamic and interactive multi-level grouping with filtering and aggregates over <b>50'000</b> items<br>
        Each grouping level can have its own aggregates (over child rows, child groups, or all descendant rows).<br>
        Personally, this is just the coolest slickest thing I've ever seen done with DHTML grids!
      </li>
    </ul>
  </div>
</div>


<script src="../lib/firebugx.js"></script>

<script src="../lib/jquery-1.7.min.js"></script>
<script src="../lib/jquery-ui-1.8.16.custom.min.js"></script>
<script src="../lib/jquery.event.drag-2.2.js"></script>

<script src="../slick.core.js"></script>
<script src="../slick.formatters.js"></script>
<script src="../slick.editors.js"></script>
<script src="../plugins/slick.cellrangedecorator.js"></script>
<script src="../plugins/slick.cellrangeselector.js"></script>
<script src="../plugins/slick.cellselectionmodel.js"></script>
<script src="../slick.grid.js"></script>
<script src="../slick.groupitemmetadataprovider.js"></script>
<script src="../slick.dataview.js"></script>
<script src="../controls/slick.pager.js"></script>
<script src="../controls/slick.columnpicker.js"></script>

<script>
var dataView;
var grid;
var data = [];
var columns = [
  {id: "sel", name: "#", field: "num", cssClass: "cell-selection", width: 40, resizable: false, selectable: false, focusable: false },
  {id: "title", name: "Title", field: "title", width: 70, minWidth: 50, cssClass: "cell-title", sortable: true, editor: Slick.Editors.Text},
  {id: "duration", name: "Duration", field: "duration", width: 70, sortable: true, groupTotalsFormatter: sumTotalsFormatter},
  {id: "%", name: "% Complete", field: "percentComplete", width: 80, formatter: Slick.Formatters.PercentCompleteBar, sortable: true, groupTotalsFormatter: avgTotalsFormatter},
  {id: "start", name: "Start", field: "start", minWidth: 60, sortable: true},
  {id: "finish", name: "Finish", field: "finish", minWidth: 60, sortable: true},
  {id: "cost", name: "Cost", field: "cost", width: 90, sortable: true, groupTotalsFormatter: sumTotalsFormatter},
  {id: "effort-driven", name: "Effort Driven", width: 80, minWidth: 20, maxWidth: 80, cssClass: "cell-effort-driven", field: "effortDriven", formatter: Slick.Formatters.Checkmark, sortable: true}
];

var options = {
  enableCellNavigation: true,
  editable: true
};

var sortcol = "title";
var sortdir = 1;
var percentCompleteThreshold = 0;
var prevPercentCompleteThreshold = 0;

function avgTotalsFormatter(totals, columnDef) {
  var val = totals.avg && totals.avg[columnDef.field];
  if (val != null) {
    return "avg: " + Math.round(val) + "%";
  }
  return "";
}

function sumTotalsFormatter(totals, columnDef) {
  var val = totals.sum && totals.sum[columnDef.field];
  if (val != null) {
    return "total: " + ((Math.round(parseFloat(val)*100)/100));
  }
  return "";
}

function myFilter(item, args) {
  return item["percentComplete"] >= args.percentComplete;
}

function percentCompleteSort(a, b) {
  return a["percentComplete"] - b["percentComplete"];
}

function comparer(a, b) {
  var x = a[sortcol], y = b[sortcol];
  return (x == y ? 0 : (x > y ? 1 : -1));
}

function groupByDuration() {
  dataView.setGrouping({
    getter: "duration",
    formatter: function (g) {
      return "Duration: " + g.value + " <span style='color:green'>(" + g.count + " items)</span>";
    },
    aggregators: [
      new Slick.Data.Aggregators.Avg("percentComplete"),
      new Slick.Data.Aggregators.Sum("cost")
    ],
    aggregateCollapsed: false
  });
}

function groupByDurationOrderByCount(aggregateCollapsed) {
  dataView.setGrouping({
    getter: "duration",
    formatter: function (g) {
      return "Duration: " + g.value + " <span style='color:green'>(" + g.count + " items)</span>";
    },
    comparer: function (a, b) {
      return a.count - b.count;
    },
    aggregators: [
      new Slick.Data.Aggregators.Avg("percentComplete"),
      new Slick.Data.Aggregators.Sum("cost")
    ],
    aggregateCollapsed: aggregateCollapsed
  });
}

function groupByDurationEffortDriven() {
  dataView.setGrouping([
    {
      getter: "duration",
      formatter :function (g) {
        return "Duration: " + g.value + " <span style='color:green'>(" + g.count + " items)</span>";
      },
      aggregators: [
        new Slick.Data.Aggregators.Sum("duration"),
        new Slick.Data.Aggregators.Sum("cost")
      ],
      aggregateCollapsed: true
    },
    {
      getter: "effortDriven",
      formatter :function (g) {
        return "Effort-Driven: " + (g.value ? "True" : "False") + " <span style='color:green'>(" + g.count + " items)</span>";
      },
      aggregators: [
        new Slick.Data.Aggregators.Avg("percentComplete"),
        new Slick.Data.Aggregators.Sum("cost")
      ],
      collapsed: true
    }
  ]);
}

function groupByDurationEffortDrivenPercent() {
  dataView.setGrouping([
    {
      getter: "duration",
      formatter: function (g) {
        return "Duration: " + g.value + " <span style='color:green'>(" + g.count + " items)</span>";
      },
      aggregators: [
        new Slick.Data.Aggregators.Sum("duration"),
        new Slick.Data.Aggregators.Sum("cost")
      ],
      aggregateCollapsed: true
    },
    {
      getter: "effortDriven",
      formatter: function (g) {
        return "Effort-Driven: " + (g.value ? "True" : "False") + " <span style='color:green'>(" + g.count + " items)</span>";
      },
      aggregators :[
        new Slick.Data.Aggregators.Sum("duration"),
        new Slick.Data.Aggregators.Sum("cost")
      ]
    },
    {
      getter: "percentComplete",
      formatter: function (g) {
        return "% Complete: " + g.value + " <span style='color:green'>(" + g.count + " items)</span>";
      },
      aggregators: [
        new Slick.Data.Aggregators.Avg("percentComplete")
      ],
      aggregateCollapsed: true,
      collapsed: true
    }
  ]);
}

function loadData(count) {
  var someDates = ["01/01/2009", "02/02/2009", "03/03/2009"];
  data = [];
  // prepare the data
  for (var i = 0; i < count; i++) {
    var d = (data[i] = {});

    d["id"] = "id_" + i;
    d["num"] = i;
    d["title"] = "Task " + i;
    d["duration"] = Math.round(Math.random() * 14);
    d["percentComplete"] = Math.round(Math.random() * 100);
    d["start"] = someDates[ Math.floor((Math.random()*2)) ];
    d["finish"] = someDates[ Math.floor((Math.random()*2)) ];
    d["cost"] = Math.round(Math.random() * 10000) / 100;
    d["effortDriven"] = (i % 5 == 0);
  }
  dataView.setItems(data);
}


$(".grid-header .ui-icon")
    .addClass("ui-state-default ui-corner-all")
    .mouseover(function (e) {
      $(e.target).addClass("ui-state-hover")
    })
    .mouseout(function (e) {
      $(e.target).removeClass("ui-state-hover")
    });

$(function () {
  var groupItemMetadataProvider = new Slick.Data.GroupItemMetadataProvider();
  dataView = new Slick.Data.DataView({
    groupItemMetadataProvider: groupItemMetadataProvider,
    inlineFilters: true
  });
  grid = new Slick.Grid("#myGrid", dataView, columns, options);

  // register the group item metadata provider to add expand/collapse group handlers
  grid.registerPlugin(groupItemMetadataProvider);
  grid.setSelectionModel(new Slick.CellSelectionModel());

  var pager = new Slick.Controls.Pager(dataView, grid, $("#pager"));
  var columnpicker = new Slick.Controls.ColumnPicker(columns, grid, options);


  grid.onSort.subscribe(function (e, args) {
    sortdir = args.sortAsc ? 1 : -1;
    sortcol = args.sortCol.field;

    if ($.browser.msie && $.browser.version <= 8) {
      // using temporary Object.prototype.toString override
      // more limited and does lexicographic sort only by default, but can be much faster

      var percentCompleteValueFn = function () {
        var val = this["percentComplete"];
        if (val < 10) {
          return "00" + val;
        } else if (val < 100) {
          return "0" + val;
        } else {
          return val;
        }
      };

      // use numeric sort of % and lexicographic for everything else
      dataView.fastSort((sortcol == "percentComplete") ? percentCompleteValueFn : sortcol, args.sortAsc);
    }
    else {
      // using native sort with comparer
      // preferred method but can be very slow in IE with huge datasets
      dataView.sort(comparer, args.sortAsc);
    }
  });

  // wire up model events to drive the grid
  dataView.onRowCountChanged.subscribe(function (e, args) {
    grid.updateRowCount();
    grid.render();
  });

  dataView.onRowsChanged.subscribe(function (e, args) {
    grid.invalidateRows(args.rows);
    grid.render();
  });


  var h_runfilters = null;

  // wire up the slider to apply the filter to the model
  $("#pcSlider,#pcSlider2").slider({
    "range": "min",
    "slide": function (event, ui) {
      Slick.GlobalEditorLock.cancelCurrentEdit();

      if (percentCompleteThreshold != ui.value) {
        window.clearTimeout(h_runfilters);
        h_runfilters = window.setTimeout(filterAndUpdate, 10);
        percentCompleteThreshold = ui.value;
      }
    }
  });


  function filterAndUpdate() {
    var isNarrowing = percentCompleteThreshold > prevPercentCompleteThreshold;
    var isExpanding = percentCompleteThreshold < prevPercentCompleteThreshold;
    var renderedRange = grid.getRenderedRange();

    dataView.setFilterArgs({
      percentComplete: percentCompleteThreshold
    });
    dataView.setRefreshHints({
      ignoreDiffsBefore: renderedRange.top,
      ignoreDiffsAfter: renderedRange.bottom + 1,
      isFilterNarrowing: isNarrowing,
      isFilterExpanding: isExpanding
    });
    dataView.refresh();

    prevPercentCompleteThreshold = percentCompleteThreshold;
  }

  // initialize the model after all the events have been hooked up
  dataView.beginUpdate();
  dataView.setFilter(myFilter);
  dataView.setFilterArgs({
    percentComplete: percentCompleteThreshold
  });
  loadData(50);
  groupByDuration();
  dataView.endUpdate();

  $("#gridContainer").resizable();
})
</script>
</body>
</html>

    Status
    API
    Training
    Shop
    Blog
    About

    © 2013 GitHub, Inc.
    Terms
    Privacy
    Security
    Contact

