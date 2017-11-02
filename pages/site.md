---
layout: page
title: ""
permalink: "/site/"
header: no
---
<script src="../assets/js/jquery.js"></script>
<script src="https://npmcdn.com/csv2geojson@latest/csv2geojson.js"></script>
<script src="../assets/js/papaparse.min.js"></script>


<div class="results"></div>


<script type="text/javascript">

// parsing function
function getUrlVars() {
  var vars = {};
  var parts = window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(m,key,value) {
    vars[key] = value;
  });
  return vars;
}

// processing function
function doStuff(data) {
    //Data is usable here
    console.log(data.indexOf() > -1);
}

// Using the jQuery library
var first = getUrlVars()["site"];

var mystring = "<img src='../images/overviews/" +  first + "_overview.png' width='250' height='250'/>"

function parseData(url, test, callBack) {
Papa.parse(url, { 
      download: true,
      header: true,
      complete: function(results) {
        callBack(results, test);
      }
      });
};

parseData('http://europhen.org/assets/data/sites.csv', first, doStuff);

$('.results').html(mystring);

</script>
	
	