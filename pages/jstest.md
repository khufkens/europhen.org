---
layout: page
title: ""
permalink: "/jstest/"
header: no
---

<div class="metadata"></div>

<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
<script type="text/javascript">

// jsonify the data in _data and provided
// by ruby (doesn't require reading in any
// new csv data
var sites = {{ site.data.sites | jsonify }};

console.log("sites");

</script>
	
	