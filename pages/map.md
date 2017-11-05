---
layout: page
title: ""
permalink: "/map/"
header: no
---

<style>
.legend {
	text-align: left;
	line-height: 18px;
	color: #555;
	padding: 6px 8px;
	font: 16px/18px Arial, Helvetica, sans-serif;
	background: rgba(255,255,255,0.8);
	box-shadow: 0 0 15px rgba(0,0,0,0.2);
	border-radius: 5px;
}

.legend h4 {
    margin: 0 0 5px;
	color: #777;
}

.legend i {
	width: 18px;
	height: 18px;
	float: left;
	margin-right: 8px;
	opacity: 0.7;
}

.legend .circle {
	border-radius: 50%;
	width: 10px;
	height: 10px;
	margin-top: 8px;

}
</style>

<link rel="stylesheet" href="../assets/css/leaflet.css" />
<script src="../assets/js/leaflet.js"></script>
<script src="https://npmcdn.com/csv2geojson@latest/csv2geojson.js"></script>
<script src="../assets/js/jquery.js"></script>
<link href='../assets/css/leaflet.fullscreen.css' rel='stylesheet' />
<script src='../assets/js/leaflet.fullscreen.min.js'></script>


<div id="mapid" style="width: 600px%; height: 750px; z-index:0;"></div>
<script type="text/javascript">

	var mymap = L.map('mapid',{fullscreenControl: true }).setView([52, 13], 4);
	L.tileLayer('http://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}.jpg',
	{	maxZoom: 18,
		attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community',
		id: 'mapbox.streets'
	}).addTo(mymap);

	$(document).ready(function() {
    $.ajax({
        type: "GET",
        url: '../assets/data/sites.csv',
        dataType: "text",
        success: function(csvData) {makeGeoJSON(csvData);}
     });
	});

function makeGeoJSON(csvData) {
    csv2geojson.csv2geojson(csvData, {
        latfield: 'lat',
        lonfield: 'lng',
        delimiter: ','
    }, function(err, data) {
      L.geoJson(data, {
    	pointToLayer: function (feature, latlng) {
        return L.circleMarker(latlng,
             {
             radius: 6,
  			 fillColor: feature.properties.colour,
    		 color: "yellow",
    		 weight: 0,
    		 opacity: 1,
    		 fillOpacity: 0.8
    		 }
         );
        },
        onEachFeature: function (feature, layer) {
                layer.bindPopup(
                '<img src="/images/overviews/' + feature.properties.shortname + '_overview.jpg"><br>' + '<b><a href="http://europhen.org/site/index.html?site=' + feature.properties.shortname + ' ">' + feature.properties.sitename + '</a></b> (' + feature.properties.shortname + ')');
        }
        }).addTo(mymap);
      
      
        });
}	
</script>
	

	
	