---
layout: main
---

The Quirkology Pace Of Life Project.

<div id="pace" class="pretty"></div>

<style>
.axis text {
  font: 10px sans-serif;
}

.axis path, .axis line {
  fill: none;
  stroke: #000;
  shape-rendering: crispEdges;
}

.bar {
  fill: #98d0cf;
}
</style>

<script>

var margin = {top: 20, right: 20, bottom: 20, left: 70},
    width = 640 - margin.left - margin.right,
    height = 450 - margin.top - margin.bottom;

    var x = d3.scale.linear()
    .range([width, 0]);

var y = d3.scale.ordinal()
    //.domain("AaBbCcDdEeFfGgHhIiJjKkLlMmNnOoPpQqRrSsTtUuVvWwXxYyZz".split(""))
    //.domain(["Singapore", "Copenhagen", "London"])
    .rangeRoundBands([0, height], .1);

var yAxis = d3.svg.axis()
    .scale(y)
    //.tickValues(x.domain().filter(function(d, i) { return !(i % 2); }))
    .orient("left");

var pace = d3.select("#pace").append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

pace.append("g")
    .attr("class", "y axis")
    .call(yAxis);

  var csv;

    d3.csv("{{ site.baseurl }}/data/pace.csv", function(error, data) {
      x.domain([0, d3.max(data, function(d) { return d.time; })]);
      //y.domain(["Singapore", "Copenhagen", "London"]);
      
      csv = [];
      data.forEach(function(d) {
        csv.push(d.city);
      });
      y.domain(csv);
      
      pace.selectAll(".bar")
        .data(data)
        .enter().append("rect")
        .attr("class", "bar")
        .attr("x", function(d) { return 0 })
        .attr("y", function(d) { return y(d.city); })
        .attr("height", y.rangeBand())
        .attr("width", function(d) { return width - x(d.time); });
            
        pace.append("g")
          .attr("class", "y axis")
          .call(yAxis);
    });

</script>
