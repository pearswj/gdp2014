---
layout: main
---

The top 20 happiest countries.

<!-- 1. Denmark
2. Norway
3. Switzerland
4. The Netherlands
5. Sweden
6. Canada
7. Finland
8. Austria
9. Iceland
10. Australia
11. Israel
12. Costa Rica
13. New Zealand
14. United Arab Emirates
15. Panama
16. Mexico
17. United States of America
18. Ireland
19. Luxembourg
20. Venzuela -->

<div id="map"></div>

_— [The United Nations Sustainable Development Solutions Network annual "World Happiness Report" for 2013](http://unsdsn.org/happiness/)_

<style>
path.country.id-208,
path.country.id-578,
path.country.id-756,
path.country.id-528,
path.country.id-752,
path.country.id-124,
path.country.id-246,
path.country.id-040,
path.country.id-352,
path.country.id-036,
path.country.id-376,
path.country.id-188,
path.country.id-554,
path.country.id-784,
path.country.id-590,
path.country.id-594, /* panama canal zone */
path.country.id-484,
path.country.id-840,
path.country.id-372,
path.country.id-442,
path.country.id-862 {
  fill: #5A9593;
}
path.country { fill: #f3f3f3; }
</style>

<script src="http://d3js.org/topojson.v1.min.js"></script>
<script>

var width = 640,
    height = 420;

var projection = d3.geo.mercator()
    .scale((width + 1) / 2 / Math.PI)
    .translate([width / 2, height / 2])
    .precision(.1);

var path = d3.geo.path()
    .projection(projection);

var graticule = d3.geo.graticule();

var svg = d3.select("#map").append("svg")
    .attr("width", width)
    .attr("height", height);

svg.append("path")
    .datum(graticule)
    .attr("class", "graticule")
    .attr("d", path);

d3.json("{{ site.baseurl }}/data/world-50m.json", function(error, world) {
  var countries = topojson.feature(world, world.objects.countries).features;

    svg.selectAll(".country")
        .data(countries)
      .enter().append("path")
        .attr("class", function(d) { return "country id-" + d.id; })
        .attr("d", path)
});

d3.select(self.frameElement).style("height", height + "px");

</script>