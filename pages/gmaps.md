---
layout: page
title: Map
subtitle: 
published: true
---
Map created with <a href="http://leafletjs.com" target="_blank">Leaflet</a>, using base layer data from <a href="https://www.mapbox.com" target="_blank">MapBox</a>.
There's a <a href="https://carlosgrohmann.com/blog/making-a-where-ive-been-map-with-leaflet/" target="_blank">post on my blog</a> explaining how to make this map.

For a more immersive experience, there's a full-screen version <a href="/pages/gmaps_full.html" target="_blank">here</a> (opens in a new tab/window).
<div>
<h4>Some interesting places I've been</h4>

<!-- JQuery -->
<script src="{{site.baseurl}}/assets/js/jquery-3.4.1.min.js"></script>

<!-- Leaflet stuff -->
<link rel="stylesheet" href="{{site.baseurl}}/assets/js/leaflet.css" />
<script src="{{site.baseurl}}/assets/js/leaflet.js"></script>
<script src="{{site.baseurl}}/assets/js/leaflet-providers.js"></script>

<!-- Leaflet Label plugin -->
<script src='{{site.baseurl}}/assets/js/leaflet.label.js'></script>
<link href='{{site.baseurl}}/assets/js/leaflet.label.css' rel='stylesheet' />

<!-- /* LeafLet map props*/ -->
<style type="text/css">
#map { height: 450px; width: 650px;}
</style>

<!-- LeafLet map  - relative link -->
<div id="map"></div>
<!-- places.geojson -->
<link rel="points" type="application/json" href='/pages/places.geojson'>
<!-- <script src='places.geojson' type="text/javascript"></script> http://{s}.tiles.mapbox.com/v4/mapbox.natural-earth-2/{z}/{x}/{y}.png-->

<!--  -->
<!-- https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png -->
<!-- https://{s}.tiles.mapbox.com/v4/mapbox.satellite/${z}/${x}/${y}.png -->



<script>
    // create map
    // var map = L.map('map').setView([15, 0], 1);
    // Basic MBox map - zooms 0-4
    // mapbox_simple = L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}', {
    //         maxZoom: 4,
    //         minZoom: 0,
    //         id: 'mapbox.streets',
    //         accessToken: 'pk.eyJ1IjoiY2FybG9zZ3JvaG1hbm4iLCJhIjoiOGNmS3ptYyJ9.WzKUdXGmEgbl4C5EdQMhMw',
    //         attribution: '&copy; Tiles Courtesy of <a href="https://www.mapbox.com" title="MapBox" target="_blank">MapBox</a>',
    //         }).addTo(map);
    // // MapBox Terrain - zooms 5-18
    // MBTerrain = L.tileLayer('http://{s}.tiles.mapbox.com/v3/carlosgrohmann.ibb4756i/{z}/{x}/{y}.png', {
    //         maxZoom: 18,
    //         minZoom: 5,
    //         attribution: '&copy; Tiles Courtesy of <a href="https://www.mapbox.com" title="MapBox" target="_blank">MapBox</a>',
    //         }).addTo(map);

    // L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}', {
    // attribution: '© <a href="https://www.mapbox.com/about/maps/">Mapbox</a> © <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a> <strong><a href="https://www.mapbox.com/map-feedback/" target="_blank">Improve this map</a></strong>',
    // tileSize: 512,
    // maxZoom: 18,
    // minZoom: 0,
    // zoomOffset: -1,
    // id: 'mapbox/satellite-streets-v11',
    // accessToken: 'pk.eyJ1IjoiY2FybG9zZ3JvaG1hbm4iLCJhIjoiOGNmS3ptYyJ9.WzKUdXGmEgbl4C5EdQMhMw'
    // }).addTo(map);


    var OpenTopoMap = L.tileLayer('https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', {
        maxZoom: 17,
        attribution: 'Map data: &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, <a href="http://viewfinderpanoramas.org">SRTM</a> | Map style: &copy; <a href="https://opentopomap.org">OpenTopoMap</a> (<a href="https://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA</a>)'
    });

    var OpenStreetMap_Mapnik = L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    });

    var Esri_WorldStreetMap = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer/tile/{z}/{y}/{x}', {
        attribution: 'Tiles &copy; Esri &mdash; Source: Esri, DeLorme, NAVTEQ, USGS, Intermap, iPC, NRCAN, Esri Japan, METI, Esri China (Hong Kong), Esri (Thailand), TomTom, 2012'
    });

    var Esri_WorldTopoMap = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/{z}/{y}/{x}', {
        attribution: 'Tiles &copy; Esri &mdash; Esri, DeLorme, NAVTEQ, TomTom, Intermap, iPC, USGS, FAO, NPS, NRCAN, GeoBase, Kadaster NL, Ordnance Survey, Esri Japan, METI, Esri China (Hong Kong), and the GIS User Community'
    });

    var Esri_WorldImagery = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
        attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community'
    });

    var Esri_WorldShadedRelief = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Shaded_Relief/MapServer/tile/{z}/{y}/{x}', {
        attribution: 'Tiles &copy; Esri &mdash; Source: Esri',
        maxZoom: 13
    });

    // color itens coording to properties
    function getColor(category) {
        return category == "airport"  ?   '#002E63' : 
               category == "place"    ?   '#FF7E00' :
               category == "dive"     ?   '#FF0000' :
                                          '#000';
    }

    // Attaching a GeoJSON file with relative link: (from: http://lyzidiamond.com/posts/osgeo-august-meeting/)
    // var places = L.layerGroup();
      $.getJSON($('link[rel="points"]').attr("href"), function(data) {
        var geoJsonLayer = L.geoJson(data, {
            onEachFeature: function (feature, layer) {
                var desc = feature.properties.Title
                layer.bindTooltip(desc)
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

    //vars for the layer control
        var otm = OpenTopoMap,
            osm  =  OpenStreetMap_Mapnik,
            ewsm = Esri_WorldStreetMap,
            ewtm = Esri_WorldTopoMap,
            ewim = Esri_WorldImagery,
            ewsr = Esri_WorldShadedRelief;


        var map = L.map('map', {
            center: [15,0],
            zoom: 1,
            layers: [ewsm]
        });

        var baseLayers = {
            "Esri WorldStreetMap": ewsm,
            "Esri WorldTopoMap": ewtm,
            "Esri WorldImagery": ewim,
            "Esri WorldShadedRelief": ewsr,
            "OpenTopo Map": otm, 
            "OpenStreetMap Mapnik": osm
        };

        // var overlays = {
        //     "Places": places
        // };

        // L.control.layers(baseLayers, overlays).addTo(map);
        L.control.layers(baseLayers).addTo(map);

</script>

&nbsp;
&nbsp;
&nbsp;
