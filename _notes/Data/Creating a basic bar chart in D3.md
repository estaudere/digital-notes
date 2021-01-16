Here's a set of code snippets that will generate a simple bar chart from a set of data in #D3. First, start by setting up your SVG object.

```
var dataset;
var w = 500;
var h = 150;
var barPadding = 1;

dataset = [ 25, 7, 5, 26, 11, 20, 25, 14 ];

var svg = d3.select("body").append("svg").attr("width", w).attr("height", h); 
```

The variables help to keep everything in line. I've listed some random numbers to serve as data as well. The flow for creating an SVG in D3 is `select` the body, `append` an SVG just on the inside, then set height and width `attr`s.

Next, you'll need to populate the SVG with your `rect`s. Start by selecting the empty, placeholder rectangles in your SVG from earlier and attaching your data to them. Then `enter` through the data—that is, actually *create* the placeholder rects you selected earlier (weird, right?).

```
var bars = svg.selectAll("rect")
	.data(dataset)
	.enter()
	.append("rect");
```

However, don't forget that **every `rect` needs a height and a width.** You'll also want to set the position so they don't overlap.

```

bars.attr("x", function(d, i) { return i * (w / dataset.length); })
	.attr("y", function(d) { return h - (d * 4); }) // "grow" from the bottom
	.attr("width", w / dataset.length - barPadding) // responsive width
	.attr("height", function(d) { return d * 4; }) // encode data as height
	.attr("fill", function(d) { return "rgb(0, 0, " + (d * 10) + ")"; }); // dual encode data as color
```

There are a couple things about SVGs you need to correct for: 

1. The x- and y-positions of the rectangles are at the top left. So, to fix this, we can set the y attribute of each rectangle to be the height of the SVG minus the height of the bar (h - d). This will "start" the rectangle where the bar is supposed to "end".
2. You can set the width and x-position of each bar to be responsive to the width of the SVG and the amount of data by setting the width attribute to the width of the SVG divded by the amount of data points (w / dataset.length) minus the amount of padding, and by setting the x attribute to data point location (i) times this new bar width (w / dataset.length).

---

*Interactive Data Visualization For The Web*, Scott Murray. #literature 