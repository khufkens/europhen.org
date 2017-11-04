---
layout: page
title: ""
permalink: "/site/"
header: no
---
<script src="../assets/js/jquery.js"></script>

<div class="image"></div>
<div class="title"></div>
<div class="metadata"></div>


<script type="text/javascript">

// jsonify the data in _data and provided
// by ruby (doesn't require reading in any
// new csv data
var sites = {{ site.data.sites | jsonify }};

console.log(sites);

// parsing function
function getUrlVars() {
  var vars = {};
  var parts = window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(m,key,value) {
    vars[key] = value;
  });
  return vars;
}

// Using the jQuery library
// grab the sitename from the url argument
var site = getUrlVars()["site"];

var imagestring = "<img src='../images/overviews/" + site + "_overview.png' width='250' height='250'/>"

$('.image').html(imagestring);

// find the index of the the site in the
// jsonified array
index = sites.findIndex(x => x.shortname == site);

console.log(index);

// use the index to subset the array
// and generate dynamic content from
// the metadata

var title = "<h1>" + sites[index].sitename + " (" + sites[index].shortname + ")" + "<\h1>";

console.log(sites[index]);

$('.title').html(title);

</script>
	
	