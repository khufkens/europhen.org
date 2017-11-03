---
layout: page
title: ""
permalink: "/site/"
header: no
---
<script src="../assets/js/jquery.js"></script>
<script src="https://npmcdn.com/csv2geojson@latest/csv2geojson.js"></script>
<script src="../assets/js/papaparse.min.js"></script>


<div class="image"></div>

<div class="title"></div>
<div class="metadata"></div>


<script type="text/javascript">

// jsonify the data in _data and provided
// by ruby (doesn't require reading in any
// new csv data
var sites = {{ site.data.sites | jsonify }};

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

// use the index to subset the array
// and generate dynamic content from
// the metadata

var title = "<h1>" + sites[index].sitename + " (" + sites[index].shortname + ")" + "<\h1>";

function makeUL(array) {
    // Create the list element:
    var list = document.createElement('ul');

    for(var i = 0; i < array.length; i++) {
        // Create the list item:
        var item = document.createElement('li');

        // Set its contents:
        item.appendChild(document.createTextNode(array[i]));

        // Add it to the list:
        list.appendChild(item);
    }

    // Finally, return the constructed list:
    return list;
}

console.log(sites[index]);

// Add the contents of options[0] to #foo:
$('.metadata').html(makeUL(sites[index]));

$('.title').html(title);



</script>
	
	