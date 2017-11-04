---
layout: page
title: ""
permalink: "/site/"
header: no
---

<div class="image"></div>
<div class="title"></div>
<div class="metadata"></div>

<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
<script type="text/javascript">

var sites = {{ site.data.sites | jsonify }};
console.log(sites);

function getUrlVars() {
  var vars = {};
  var parts = window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(m,key,value) {
    vars[key] = value;
  });
  return vars;
}

var site = getUrlVars()["site"];

var imagestring = "<img src='../images/overviews/" + site + "_overview.png' width='250' height='250'/>"

$('.image').html(imagestring);

index = sites.findIndex(x => x.shortname == site);

console.log(index);

var title = "<h1>" + sites[index].sitename + " (" + sites[index].shortname + ")" + "<\h1>";

console.log(sites[index]);

$('.title').html(title);

</script>
	
	