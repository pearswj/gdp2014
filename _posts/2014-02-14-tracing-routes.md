---
layout: main
---

A little side-study using public data from [RunKeeper](http://runkeeper.com/search/routes/1?distance=&lon=-0.139&location=fitzrovia%2C+london&activityType=RUN&lat=51.522) to map movement by <span style="color: #5a9593">bike</span> and by <span style="color: #98d0cf">foot</span> through [Fitzrovia](http://en.wikipedia.org/wiki/Fitzrovia) and the surrounding areas.

<link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.7.2/leaflet.css" />

<style>
  #tracer {
      height: 420px;
      width: 640px;
  }
</style>

<div id="tracer"></div>

It's clear from this (and from standing in the street!) that lots of people pass through this area every day. That's a large number of lives that we can affect with our proposals.

<script src="{{ site.baseurl }}/js/leaflet.js"></script>
<script>
	var map = L.map('tracer').setView([51.5181, -0.1357], 14);
  /*
	L.tileLayer('http://{s}.tile.stamen.com/toner-lite/{z}/{x}/{y}.png', {
  	attribution: 'Map tiles by <a href="http://stamen.com">Stamen Design</a>, <a href="http://creativecommons.org/licenses/by/3.0">CC BY 3.0</a> &mdash; Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
  	subdomains: 'abcd',
  	minZoom: 0,
  	maxZoom: 20
  }).addTo(map);
  */
  L.tileLayer('http://server.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Light_Gray_Base/MapServer/tile/{z}/{y}/{x}', {
  	attribution: 'Tiles &copy; Esri &mdash; Esri, DeLorme, NAVTEQ',
    minZoom: 12,
  	maxZoom: 16
  }).addTo(map);

  var geojson;
  var runStyle = {
      "color": "#98d0cf",
      "weight": 1.5,
      "opacity": 0.4
  };
  
  $.getJSON("{{ site.baseurl }}/data/runners.geojson", function(data) {
    geojson = data;
    L.geoJson(data, {
      style: runStyle
    }).addTo(map);
  });
  
  var bikeStyle = {
      "color": "#5a9593",
      "weight": 1.5,
      "opacity": 0.4
  };
  
  $.getJSON("{{ site.baseurl }}/data/cyclists.geojson", function(data) {
    geojson = data;
    L.geoJson(data, {
      style: bikeStyle
    }).addTo(map);
  });
</script>