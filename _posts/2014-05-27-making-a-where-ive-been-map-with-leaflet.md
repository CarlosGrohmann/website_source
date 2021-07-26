---
layout: post
title: Making a "where I've been" map with Leaflet
author: CarlosGrohmann
date: 2014-05-27
categories: 
tags: map javascript html json mapbox 
permalink: /blog/making-a-where-ive-been-map-with-leaflet/
published: true
---

In my website I have a map of some (most? all?) of the places I've been [here](http://carlosgrohmann.com/gmaps.html). When I first started with this idea (in 2011, I guess), I used [GoogleMaps API](https://developers.google.com/maps/) and all the points of the map had to be defined in the HTML file, which was very annoying and not very good in terms of maintenance.  

Then I discovered [MapBox](https://www.mapbox.com) and [TileMill](https://www.mapbox.com/tilemill/), and my life changed. TileMill is a very nice software for creating maps, and you can export the results to your free MapBox account, and have your map on-line in no time. The problem is: if I wanted to update the 'database' of places, I'd have to re-import it into TileMill, re-export the project and re-import it into my MapBox account. Too much hassle.  

So I decided to try something different. I wanted to be able to save/export my 'database' (a simple spreadsheet) whenever I updated it, and the map would also be updated without additional steps.  

After a little bit of Googling, I had a few options: Leaflet, Mapbox and CartoDB. [Leaflet])(http://leafletjs.com) is an open-source JavaScript library for mobile-friendly maps, MapBox is a well-know an open source mapping platform and provide the JavaScript library mapbox.js (a [plugin](https://www.mapbox.com/help/mapboxjs-a-leaflet-plugin/) that extends Leaflet's functionalities), while [CartoDB](https://cartodb.com) is "a cloud-based solution for all your mapping needs". Both MapBox and CartoDB offer free accounts (with limits on storage/views/etc).  

With CartoDB it is really simple to import a CSV file (or a lot of other formats) into a table, create a beautiful visualisation of the data, and make it public, share it, etc. I think that CartoDB is easier to maintain than MapBox, since they offer some nice tools to simply update your data (table). But for me, it has the same disadvantage of MapBox: I have to login to the site and upload/update my data.  

I didn't want to keep my data in another server. I prefer to upload a text file to the same server where my site is hosted. Even if that requires converting (from, say, CSV to GeoJSON or whatever), because I can put all that into a script. And I like scripts. <a title="Obligatory XKCD mention" href="http://xkcd.com/1319/" target="_blank">They save us time.</a>  

So I decided to use Leaflet. I'll show you how I did it.  

First, the entire HTML code:  

```html
<pre class="prettyprint linenums"><!-- JQuery -->
<script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>

<!-- Leaflet stuff -->
    <link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.css">
<script src="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.js"></script>

<!-- Leaflet Label plugin -->
<script src="https://api.tiles.mapbox.com/mapbox.js/plugins/leaflet-label/v0.2.1/leaflet.label.js"></script>
    <link href="https://api.tiles.mapbox.com/mapbox.js/plugins/leaflet-label/v0.2.1/leaflet.label.css" rel="stylesheet">

<!-- /* LeafLet map props*/ -->
<style type="text/css">
#map { height: 350px; width: 500px;}
</style>

<!-- LeafLet map  - relative link -->

<div id="map"></div>

<!-- places.geojson -->
    <link rel="points" type="application/json" href="places.geojson">
<!-- <script src='places.geojson' type="text/javascript"></script> -->

<script>
    // create map
    var map = L.map('map').setView([15, 0], 1);
    // Natural Earth - zooms 0-6
    naturalEarth = L.tileLayer('http://{s}.tiles.mapbox.com/v3/mapbox.natural-earth-2/{z}/{x}/{y}.png', {
            maxZoom: 4,
            minZoom: 0,
            attribution: '&copy; Tiles Courtesy of <a href="https://www.mapbox.com" title="MapBox" target="_blank">MapBox</a>',
            }).addTo(map);
    // MapBox Terrain - zooms 7-18
    MBTerrain = L.tileLayer('http://{s}.tiles.mapbox.com/v3/carlosgrohmann.ibb4756i/{z}/{x}/{y}.png', {
            maxZoom: 18,
            minZoom: 5,
            attribution: '&copy; Tiles Courtesy of <a href="https://www.mapbox.com" title="MapBox" target="_blank">MapBox</a>',
            }).addTo(map);                
    // color itens coording to properties
    function getColor(category) {
        return category == "airport"  ?   '#002E63' : 
               category == "place"    ?   '#FF7E00' :
                                         '#000';
    }
    // Attaching a GeoJSON file with relative link: (from: http://lyzidiamond.com/posts/osgeo-august-meeting/)
      $.getJSON($('link[rel="points"]').attr("href"), function(data) {
        var geoJsonLayer = L.geoJson(data, {
            onEachFeature: function (feature, layer) {
                var desc = feature.properties.Title
                layer.bindLabel(desc)
            },
            pointToLayer: function (feature, latlng) {
                return L.circleMarker(latlng, {
                radius: 3,
                Label: getColor(feature.properties.Title), 
                fillColor: getColor(feature.properties.category), 
                color: "#000",
                weight: 0.5,
                opacity: 0.8,
                fillOpacity: 0.8,})
            },
        });
        geoJsonLayer.addTo(map);
      });
</script>
</pre>
```

Now let's see what each part does.

The first thing to do is to call the needed libraries. In the `head` section of your file, insert these lines to access `leaflet.js`, `JQuery` and the leaflet plugin `Leaflet.label`.

```html
<pre class="prettyprint linenums"><!-- JQuery -->
<script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>

<!-- Leaflet stuff -->
    <link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.css">
<script src="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.js"></script>

<!-- Leaflet Label plugin -->
<script src="https://api.tiles.mapbox.com/mapbox.js/plugins/leaflet-label/v0.2.1/leaflet.label.js"></script>
    <link href="https://api.tiles.mapbox.com/mapbox.js/plugins/leaflet-label/v0.2.1/leaflet.label.css" rel="stylesheet">
</pre>
```

Next we need to define some basic properties for our map:  

```html
<pre class="prettyprint linenums"><!-- /* LeafLet map props*/ -->
<style type="text/css">
#map { height: 350px; width: 500px;}
</style>
<!-- LeafLet map  - relative link -->

<div id="map"></div>

</pre>
```

Now the fun begins. In my case, I opt for using a GeoJSON file with the places I've been. To create this file you need to:  
1 - export it from spreadsheet as CSV  
2 - open it in [QGIS](https://www.qgis.org)
3 - save as GeoJSON  
4 - simple, right?  

OK, now that we have the GeoJSON file, we need to do some tricks to open it directly (you can make it a JavaScript file by manually editing it, by it goes against our initial idea). The trick is to reference it in the HTML as a relative link (I got the idea from this [post](http://lyzidiamond.com/posts/osgeo-august-meeting/)). In this example, the `places.geojson` file is in the same directory as the hmtl file.  

```html
<pre class="prettyprint linenums"><!-- places.geojson -->
    <link rel="points" type="application/json" href="places.geojson">
</pre>
```

Good. Time to create the base layers of the map. I used two layers from MapBox, one from NaturalEarth (for the smaller zooms) and the other is from my personal account (you should have your account as well).  

```html
<pre class="prettyprint linenums"><script>
    // create map
    var map = L.map('map').setView([15, 0], 1);
    // Natural Earth - zooms 0-6
    naturalEarth = L.tileLayer('http://{s}.tiles.mapbox.com/v3/mapbox.natural-earth-2/{z}/{x}/{y}.png', {
            maxZoom: 4,
            minZoom: 0,
            attribution: '&copy; Tiles Courtesy of <a href="https://www.mapbox.com" title="MapBox" target="_blank">MapBox</a>',
            }).addTo(map);
    // MapBox Terrain - zooms 7-18
    MBTerrain = L.tileLayer('http://{s}.tiles.mapbox.com/v3/carlosgrohmann.ibb4756i/{z}/{x}/{y}.png', {
            maxZoom: 18,
            minZoom: 5,
            attribution: '&copy; Tiles Courtesy of <a href="https://www.mapbox.com" title="MapBox" target="_blank">MapBox</a>',
            }).addTo(map);                
    // color itens coording to properties
    function getColor(category) {
        return category == "airport"  ?   '#002E63' : 
               category == "place"    ?   '#FF7E00' :
                                         '#000';
    }
</pre>
<p>
```

And then is just a matter of reading the GeoJSON file. Well, actually, there's a bit more to it. The first part of the code (`getJSON`) reads the GeoJSON file and binds the "Title" property (column) to a popUp, which will appear as the mouse hovers over the symbols, thanks to the `Leaflet.label` plugin.  

The second part (`pointToLayer`) will create circle markers for each feature in the GeoJSON file. It will use the color defined in the `getColor` function.  

```html
<pre class="prettyprint linenums">
    // Attaching a GeoJSON file with relative link: (from: http://lyzidiamond.com/posts/osgeo-august-meeting/)
      $.getJSON($('link[rel="points"]').attr("href"), function(data) {
        var geoJsonLayer = L.geoJson(data, {
            onEachFeature: function (feature, layer) {
                var desc = feature.properties.Title
                layer.bindLabel(desc)
            },
            pointToLayer: function (feature, latlng) {
                return L.circleMarker(latlng, {
                radius: 3,
                Label: getColor(feature.properties.Title), 
                fillColor: getColor(feature.properties.category), 
                color: "#000",
                weight: 0.5,
                opacity: 0.8,
                fillOpacity: 0.8,})
            },
        });
        geoJsonLayer.addTo(map);
      });
</script>
</pre>
```

One thing to note is that in the `pointToLayer` function, one can replace the `getColor` function with a [one-line](http://blog.thematicmapping.org/2012/10/mapping-new-zealand-where-are-hot-and.html) statement (as noted in the code comments), so fell fee to use it that way, I just used the `getColor` function here because I think it's easier to understand (if you are not familiar with coding).  

And here's the final map!  

<!-- JQuery -->
<script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>

<!-- Leaflet stuff -->
<link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.css" />
<script src="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.js"></script>

<!-- Leaflet Label plugin -->
<script src='https://api.tiles.mapbox.com/mapbox.js/plugins/leaflet-label/v0.2.1/leaflet.label.js'></script>
<link href='https://api.tiles.mapbox.com/mapbox.js/plugins/leaflet-label/v0.2.1/leaflet.label.css' rel='stylesheet' />

<!-- /* LeafLet map props*/ -->
<style type="text/css">
#map { height: 450px; width: 650px;}
</style>

<!-- LeafLet map  - relative link -->
<div id="map"></div>
<!-- places.geojson -->
<link rel="points" type="application/json" href='/places.geojson'>
<!-- <script src='places.geojson' type="text/javascript"></script> -->

<script>
    // create map
    var map = L.map('map').setView([15, 0], 1);
    // Natural Earth - zooms 0-6
    naturalEarth = L.tileLayer('http://{s}.tiles.mapbox.com/v3/mapbox.natural-earth-2/{z}/{x}/{y}.png', {
            maxZoom: 4,
            minZoom: 0,
            attribution: '&copy; Tiles Courtesy of <a href="https://www.mapbox.com" title="MapBox" target="_blank">MapBox</a>',
            }).addTo(map);
    // MapBox Terrain - zooms 7-18
    MBTerrain = L.tileLayer('http://{s}.tiles.mapbox.com/v3/carlosgrohmann.ibb4756i/{z}/{x}/{y}.png', {
            maxZoom: 18,
            minZoom: 5,
            attribution: '&copy; Tiles Courtesy of <a href="https://www.mapbox.com" title="MapBox" target="_blank">MapBox</a>',
            }).addTo(map);                
    // color itens coording to properties
    function getColor(category) {
        return category == "airport"  ?   '#002E63' : 
               category == "place"    ?   '#FF7E00' :
                                         '#000';
    }
    // Attaching a GeoJSON file with relative link: (from: http://lyzidiamond.com/posts/osgeo-august-meeting/)
      $.getJSON($('link[rel="points"]').attr("href"), function(data) {
        var geoJsonLayer = L.geoJson(data, {
            onEachFeature: function (feature, layer) {
                var desc = feature.properties.Title
                layer.bindLabel(desc)
            },
            pointToLayer: function (feature, latlng) {
                return L.circleMarker(latlng, {
                radius: 3,
                Label: getColor(feature.properties.Title), 
                fillColor: getColor(feature.properties.category), 
                color: "#000",
                weight: 0.5,
                opacity: 0.8,
                fillOpacity: 0.8,})
            },
        });
        geoJsonLayer.addTo(map);
      });
</script>
&nbsp;
&nbsp;
&nbsp;

