## Mapbox javascript examples
Other than the leaflet, you have several other options to create interactive and dynamic web-based geovisualization, OpenLayer, Google Maps API, Bing Maps API, and Mapbox JS. This class, I am going to walk you be familar wit Mapbox JS. 

The Mapbox JS has a very good documentation, therefore, here I am not going to repeat the documentation. I am here to provide you some good examples, you should understand and try if you want to use MapBox for your future geovisualization project. 

1. Hello world of MapBox
This is an example of creating your first MapBox based geovisualization. This example just dispaly your map on a webpage using MapBox. ([link](https://docs.mapbox.com/mapbox-gl-js/example/simple-map/))

2. Add a marker to your map
We already talked about how to add a marker on the map using Leaflet. We can also do similar thing in MapBox. Here is the example to create marker using MapBox. ([link](https://docs.mapbox.com/mapbox-gl-js/example/add-a-marker/))

3. Add geojson to your map
Just like Leaflet, you can also use MapBox to add the GeoJson file into your map. This example show you how to add the GeoJson to your map. ([link](https://docs.mapbox.com/mapbox-gl-js/example/geojson-polygon/))

4. Create choroplth map using MapBox
In the previous example, we just add the GeoJson file into the map, we have not styled different features based on their attribute. 

```{html}


<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Load data from an external GeoJSON file</title>
<meta name="viewport" content="initial-scale=1,maximum-scale=1,user-scalable=no">
<link href="https://api.mapbox.com/mapbox-gl-js/v2.5.1/mapbox-gl.css" rel="stylesheet">
<script src="https://api.mapbox.com/mapbox-gl-js/v2.5.1/mapbox-gl.js"></script>
<style>
body { margin: 0; padding: 0; }
#map { position: absolute; top: 0; bottom: 0; width: 100%; }
</style>
</head>
<body>
<div id="map"></div>
 
<script>
	mapboxgl.accessToken = 'pk.eyJ1IjoieGlhb2ppYW5nZ2lzIiwiYSI6ImNrNnI5ZzJmcDAxNWszbW9mMjV1bGxsb3oifQ.O2EHW7BWQ3-qjo_u7ddqNA';
	const map = new mapboxgl.Map({
		container: 'map', // container ID
		style: 'mapbox://styles/mapbox/light-v10', // style URL
		zoom: 10, // starting zoom
		center: [-75.15483081704296,39.98771088576627] // starting center
	});
	
	map.on('load', () => {
		map.addSource('bloodlead', {
			type: 'geojson',
			// Use a URL for the value for the `data` property.
			data: 'blood_lead.geojson'
		});

		// Add a new layer to visualize the polygon.
		map.addLayer({
			'id': 'bloodlead-polygon',
			'type': 'fill',
			'source': 'bloodlead', // reference the data source
			'layout': {},
			'paint': {
				'fill-color': {
	              property: 'perc_5plus',
	              stops: [
	                [5, "#dee5e5"], 
	                [10, "#e31a1c"],
	                [15, "#fd8d3c"],
	                [20, "#fecc5c"],
	                [21, "#ffffb2"],
	                [22, '#33a02c']
	              ]
				}, // blue color fill
				'fill-opacity': 0.5
			}
		});

		map.addLayer({
			'id': 'bloodlead-bound',
			'type': 'line',
			'source': 'bloodlead',
			'paint': {'line-color': '#000',
			'line-width': 1
			}
			});
	});

</script>
 
</body>
</html>


```




