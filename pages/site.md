---
layout: page-fullwidth
title: ""
permalink: "/site/"
header: no
---
<div class = "row">
	<div class = "medium-3 columns image"></div>
	<div class="medium-9 columns content"></div>
</div>
<div class = "row">
	<br>
	<div class="medium-12 columns" id="plot"></div>
	<br>
</div>

<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
<script src="https://cdn.plot.ly/plotly-1.2.0.min.js"></script>

<script type="text/javascript">

var sites = {{ site.data.sites | jsonify }};

function getUrlVars() {
  var vars = {};
  var parts = window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(m,key,value) {
    vars[key] = value;
  });
  return vars;
}

var site = getUrlVars()["site"];
index = sites.findIndex(x => x.shortname == site);

var title = "<h1>" + sites[index].sitename + " (" + sites[index].shortname + ")" + "</h1>";
var species = "<b>Vegetation Type: </b>" + sites[index].species + "<br>";
var latitude = "<b>Latitude: </b>" + sites[index].lat + "<br>";
var longitude = "<b>Longitude: </b>" + sites[index].long + "<br>";
var country = "<b>Country: </b>" + sites[index].country + "<br>";
var camera = "<b>Camera Type: </b>" + sites[index].camera + "<br>";

var content = title + species + country + latitude + longitude + camera;

var imagestring = "<img src='../images/overviews/" + site + "_overview.png' width='250' height='250'/>";

$('.image').html(imagestring);
$('.content').html(content);

var data = "{{site.url}}" + "/assets/data/" + site + ".csv";

console.log(data);

Plotly.d3.csv(data, function(rows){
    var gcc = {
      type: 'scatter',                    // set the chart type
      mode: 'lines',                      // connect points with lines
      name: 'Gcc',
      x: rows.map(function(row){          // set the x-data
        return row['date'];
      }),
      y: rows.map(function(row){          // set the x-data
        return row['gcc'];
      }),
      line: {
        color: 'green',
        width: 1
      }
    };

    var rcc = {
      type: 'scatter',                    // set the chart type
      mode: 'lines',                      // connect points with lines
       name: 'Rcc',
      x: rows.map(function(row){          // set the x-data
        return row['date'];
      }),
      y: rows.map(function(row){          // set the x-data
        return row['rcc'];
      }),
      line: {
        color: 'red',
        width: 1
      }
    };

    var bcc = {
      type: 'scatter',                    // set the chart type
      mode: 'lines',                      // connect points with lines
      name: 'Bcc',
      x: rows.map(function(row){          // set the x-data
        return row['date'];
      }),
      y: rows.map(function(row){          // set the x-data
        return row['bcc'];
      }),
      line: {
        color: 'blue',
        width: 1
      }
    };
    
    var layout = {
      yaxis: {title: "Chromatic Coorindate (Gcc/Rcc/Bcc)"},       // set the y axis title
      xaxis: {
        showgrid: false,                  // remove the x-axis grid lines
        tickformat: "%Y-%m-%d"              // customize the date format to "month, day"
      },
      margin: {                           // update the left, bottom, right, top margin
        l: 100, b: 50, r: 50, t: 50
      }
    };

    Plotly.plot(document.getElementById('plot'), [bcc, rcc, gcc], layout, {showLink: false});
});


</script>
	
	