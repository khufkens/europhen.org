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

// Using the jQuery library
var first = getUrlVars()["site"];

var mystring = "<img src='/images/overviews/" +  first + "_overview.png' width='250' height='250'/>"

$('.results').html(mystring);

</script>
	
	