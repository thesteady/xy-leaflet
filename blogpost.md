potential titles:
# How To Use Leaflet Without A Projection
# How To Map X, Y Coordinates in Leaflet
# How To Use Leaflet For X, Y Points


## Intro
- what are projections, when would we want to NOT use them?
- why do this? use cases
- why leaflet and not something else (d3)?
- what is a "slippy map" anyway?

Have you ever wanted to display x-y data points on your site? There are lots of tools to get the job done! Maybe you need a simple graph with two axes. [D3.js](https://d3js.org/) or [Highcharts](http://www.highcharts.com/) would probably work fine. Want your user to be able to interact with those points? Zoom in/out? What about panning around? These things all feel reasonable with D3.js. Mike Bostock even has example blocks: [a map with zooming and panning](https://bl.ocks.org/mbostock/eec4a6cda2f573574a11) and [a second version](http://bl.ocks.org/mbostock/09dd5ad7d6bfd40187e0). Cool, huh? But what if we wanted something a little different? What if we didn't want to handle writing code for managing zoom/pan? **What if we wanted a custom background under our points?**

I was curious what it would be like to create a display of x-y points on a slippy map using Leaflet.js. [Leaflet.js](http://leafletjs.com) is a popular open-source library for creating and displaying maps on the web. Leaflet is a great tool for making real-world maps with your geospatial data, but I was unsure how it would work with _unprojected_ data -- data without a geographical component. This post will walk you through how to make it work (_Spoiler alert: it's EASY), and then a few things we can do to customize it a bit more.

## Before We Start

### Get To Know Leaflet.js
If you're not familiar with Leaflet already, I recommend checking out the [Quick Start Guide](http://leafletjs.com/examples/quick-start.html) and [Tutorials](http://leafletjs.com/examples.html) to get a feel for the API. I'll reference documentation throughout the walkthrough, though, so if you like to live a little dangerously, keep readin'!

### Maps Primer: What are Projections?
When working with geospatial data (e.g., GPS points with a latitude and longitude), we have to consider how to display points that are really from a three-dimensional surface (the earth) on a two-dimensional surface. A map _projection_ is what we use to make that translation happen! There are lots of different projections, each with their own tradeoffs. For example, some projections are designed to display specific areas of the world with minimal distortion. The further away from the focus area you get, the more distortion you see. **example about US distortion?**. Other projections might distort shapes or distances. If you mostly look at maps on the web, then you're probably most familiar with the [Web Mercator projection](https://en.wikipedia.org/wiki/Web_Mercator). It's a variation of the [Mercator projection](https://en.wikipedia.org/wiki/Mercator_projection). A common way of thinking about the translation that Mercator does is: turn the three-dimensional globe onto a cylinder, and then lay it flat onto two-dimensional space. The Mercator projection minimizes distortion at the equator and maximizes distortion at the poles. This makes places like Antarctica and Greenland look much bigger than they really are relative to more equatorial geographies.

How do we compare different points on the ground? Well, to make things more complicated, in addition to different projection systems, there are also different _coordinate systems_. We can ignore coordinate systems for this exercise, but I encourage you to learn more about them if you're interested in mapping.

In this example, we want our data to be **unprojected**. This means we want to make sure that Leaflet.js does not apply the Web Mercator projection, which is the default setting.

## Let's Try It Out!
** Want to see the finished code for this project? Check it out on [GitHub](https://github.com/thesteady/xy-leaflet).**

To explore how an unprojected web map works in Leaflet, let's use a simple set-up. First, we'll need an `index.html` file with the basic structure like so:

```
<html>
	<head>
		<link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet/v0.7.7/leaflet.css" />
  		<script src="http://cdn.leafletjs.com/leaflet/v0.7.7/leaflet.js"></script>
	</head>
	<body>
		<div id="map"></div>
		<script type="text/javascript">
			// our map JavaScript will go here.
		</script>
	</body>
</html>
```

We've pulled in Leaflet.js via CDN, created a specific div for our map, and added a script tag where we will write our JavaScript. Inside that script tag, we'll first instantiate our map:

```
var map = L.map('map', {}).setView([5, 1], 4);
```
We pass the `id` of the div we want to use for our map as well as an options object. For the moment, let's not set anything special. What about those numbers in the `setView` call? The array represents our starting center point - the location at which we want the map to be centered on page load. The last parameter, "4", is the initial zoom level.

If you load your `index.html` in a browser at this point, you'll get a whopping dissapoint: no map! But, inspecting the HTML, you'll see that it's there, just not visible. We need to set some styling on it to make it appear. Inside the `<head>` of your HTML, add the following styling:

```
<style>
	 #map {
      height: 500px;
    }
    .leaflet-container {
      background-color: #eee;
      border: 1px solid #888;
    }
</style>
```

This will give our map a height, a background color, and a border. Try refreshing the page, and you should see your map!



- what's the key to no projection? OH SNAP ITS EAAAASSSY.

- lets add some points

We have a basemap, but does it actually work the way we expect it to? Let's add some points to find out! Let's use a simple case of a few easy-to-think-about points:
```
<- POINTS GO HERE->
var points = []
```

Now that we've defined our point set, let's add them to the map. While we're doing this, we'll add a popup on the markers so that we can check out exactly which point it is.
```
<-add points to map ->
```

- check it out visually

Now reload your page in the browser. Wow! This is what you should see:
<- Screenshot of map at this point.->

- lets add MOAR POINTS
- link to leaflet docs a lot
- mention mounting all the points individually vs. as a layer (performance concerns?)
- link to my github repo

## Adding a Custom Basemap
- add a custom basemap. maybe 4 differently colored quadrants so we can see what "area" we're exploring?

## Summary
- reiterate why
- fun challenges: what else could you do with this?
- reference for learning more or diving deeper
