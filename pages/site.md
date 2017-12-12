---
layout: page
title: ""
permalink: "/site/"
header: no
---
<div class = "row">
	<div class = "medium-4 columns image"></div>
	<div class="medium-8 columns content"></div>
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

var imagestring = "<img src='../images/overviews/" + site + "_overview.jpg' width='250' height='250'/>";

$('.image').html(imagestring);
$('.content').html(content);

var data = "{{site.url}}" + "/assets/data/" + site + ".csv";

Plotly.d3.csv(data, function(rows){
    var gcc = {
      type: 'scatter',                    
      mode: 'lines',                      
      name: 'Gcc',
      x: rows.map(function(row){          
        return row['date'];
      }),
      y: rows.map(function(row){          
        return row['gcc'];
      }),
      line: {
        color: 'green',
        width: 1
      }
    };

    var rcc = {
      type: 'scatter',                    
      mode: 'lines',                      
       name: 'Rcc',
      x: rows.map(function(row){          
        return row['date'];
      }),
      y: rows.map(function(row){          
        return row['rcc'];
      }),
      line: {
        color: 'red',
        width: 1
      }
    };

    var bcc = {
      type: 'scatter',                    
      mode: 'lines',                      
      name: 'Bcc',
      x: rows.map(function(row){          
        return row['date'];
      }),
      y: rows.map(function(row){          
        return row['bcc'];
      }),
      line: {
        color: 'blue',
        width: 1
      }
    };
    
    var layout = {
      yaxis: {title: "Chromatic Coorindate (Gcc/Rcc/Bcc)"},       
      xaxis: {
        showgrid: false,                  
        tickformat: "%Y-%m-%d"              
      },
      margin: {                           
        l: 100, b: 50, r: 50, t: 50
      }
    };

    Plotly.plot(document.getElementById('plot'), [bcc, rcc, gcc], layout, {showLink: false});
});

</script>
	
	
