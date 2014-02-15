The Quirkology Pace Of Life Project.

<div id="pie" class="pretty"></div>

<script>
  var width = 300,
      height = 280,
      radius = Math.min(width, height) / 2;
  
  var color = d3.scale.ordinal()
      .range(["#5A9593", "#98D0CF"]);
  
  var arc = d3.svg.arc()
      .outerRadius(radius - 10)
      .innerRadius(radius - 40);
  
  var pie = d3.layout.pie()
      .sort(null)
      .value(function(d) { return d.population; });
  
  var svg_pie = d3.select("body").select("#pie").append("svg")
      .attr("width", width)
      .attr("height", height)
    .append("g")
      .attr("transform", "translate(" + width / 2 + "," + height / 2 + ")");
  
  d3.csv("{{ site.baseurl }}/data/stress.csv", function(error, data) {
  
    data.forEach(function(d) {
      d.population = +d.population;
    });
  
    var g = svg_pie.selectAll(".arc")
        .data(pie(data))
      .enter().append("g")
        .attr("class", "arc");
  
    g.append("path")
        .attr("d", arc)
        .style("fill", function(d) { return color(d.data.stressed); });
  
    //g.append("text")
    //    .attr("transform", function(d) { return "translate(" + arc.centroid(d) + ")"; })
    //    .attr("dy", ".35em")
    //    .style("text-anchor", "middle")
    //    .text(function(d) { return d.data.population + "%"; });
  
  });
  
  var arc2 = d3.svg.arc()
      .outerRadius(radius - 50)
      .innerRadius(radius - 80);
  
  d3.csv("{{ site.baseurl }}/data/worry.csv", function(error, data) {
  
    data.forEach(function(d) {
      d.population = +d.population;
    });
  
    var g = svg_pie.selectAll(".arc2")
        .data(pie(data))
      .enter().append("g")
        .attr("class", "arc2");
  
    g.append("path")
        .attr("d", arc2)
        .style("fill", function(d) { return color(d.data.worry); });
  
  });
  
  var arc3 = d3.svg.arc()
      .outerRadius(radius - 90)
      .innerRadius(radius - 120);
  
  d3.csv("{{ site.baseurl }}/data/anxiety.csv", function(error, data) {
  
    data.forEach(function(d) {
      d.population = +d.population;
    });
  
    var g = svg_pie.selectAll(".arc3")
        .data(pie(data))
      .enter().append("g")
        .attr("class", "arc3");
  
    g.append("path")
        .attr("d", arc3)
        .style("fill", function(d) { return color(d.data.anxiety); });
  
  });
</script>
