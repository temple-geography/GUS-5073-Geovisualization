# Week 8. Introduction of Javascripts/HTML/CSS
This week we are going to first use Javascripts/HTML/CSS to write our first web-based geovisualization. You will know how to add marker, line, and polygon on map instance using Lealet.js. 

### HTML/CSS/JavaScript

Most websites are based on three core technologies: HTML, CSS, and JavaScript. HTML stands for HyperText Markup Language; it is the lingua franca of web documents. It allows you to write structured content in a way that web browsers will understand. CSS stands for Cascading Style Sheet and provides a means to style a website using structure written into the document using HTML. Javascript is the web's preferred programming language and is supported by all browsers without additional plugins. We'll be using it to build interactive visualizations and web pages. JavaScript is extended by a huge number of libraries; we'll be doing our data visualization work in Leaflet.js, Mapbox.js, etc.


### 1. First blank web page
```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>Leaflet Map</title>
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css"/>
</head>
<body>

</body>
</html>
```
You will then create a blank webpage. You can save the file into `leafletExample.html`. We are going to add more elements to the page. 

## 2. Add the css and js libraries. 
This is just like what we did to import Python modules before. Add `link` tag for `css` library to the `head` part. Add the `script` tag to the `body` part. 
#### Now you code would like this.

``` html
<!DOCTYPE html>
    <html>
    <head>
    	<meta charset="utf-8">
    	<title>Leaflet Map</title>
    	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css"/>
    </head>
    <body>
        <!-- Our web map and content will go here -->
        <script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
    </body>
</html>
```
### 3. Add a Map instance to the page
After import the library for jQuery and leaflet.js, we can create map instance and create our first HTML/CSS/JavaScript webmap. 

#### Add a map `div`
Add a `div` to the body that will hold the map. This is just like any other div element we might use. We will set the style right in the div using the style attribute, and not the CSS file, otherwise all map divs we create will have the same styling.

```html
<div id="map" style="width: 1000px; height: 600px"></div>
```

#### Add map instance
Now we can create a `script` container to include our JavaScript code just below the map div
```js
var map = L.map('map', {center: [39.981192, -75.155399], zoom: 10}); // create a map instance with center of Temple University
L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', { attribution: '© OpenStreetMap' }).addTo(map);
map.doubleClickZoom.disable(); // disable the double click to zoom in
```

**Now you code look like this**
```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>Leaflet Map</title>
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css"/>
</head>
<body>
    <!-- Our web map and content will go here -->
    <script src="https://unpkg.com/leaflet@1.0.3/dist/leaflet.js"></script>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
    <div id="map" style="width: 1000px; height: 600px">
    </div>
    <script>
    	var map = L.map('map', {center: [39.981192, -75.155399], zoom: 10});
    	L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', { attribution: '© OpenStreetMap' }).addTo(map);
    	map.doubleClickZoom.disable();
    </script>
</body>
</html>
```

**Note** there are many types of tiles, you can select other types of tiles as your basemap. Here is the ([link](https://leaflet-extras.github.io/leaflet-providers/preview/)). What you need to do is to just copy the link of your favorite tile and replace the "https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png" in second line of the script division. 

Let's then open your `.html` file to see what you get. 

#### 4. Add a marker to the map instance
Just like what we did using Folium, we can create a marker in JavaScript. Add the following statement in your `script` tag after the above code. 
```js
// add point marker
var myDataPoint = L.marker([39.981192, -75.155399]).addTo(map);
myDataPoint.bindPopup("This is Temple University.");
myDataPoint.bindPopup("<h3>Temple University</h3><p>Philadelphia, PA<br>Information about Temple University.</p>");
```

The above statement will add a marker, add to the map instance, and add a popup. 

#### 5. Add a line to the map instance

You can also add a line to the map instance. This is also very similar. 
```js
// create a polyline
var myDataLine = L.polyline([[40.080922, -75.207875], 
				[40.077375, -75.201967],
				[40.073474, -75.196917],
				[40.065221, -75.191110],
				[40.062765, -75.185204],
				[40.060498, -75.178856],
				[40.051092, -75.171567],
				[40.037719, -75.171922],
				[40.036117, -75.161619],
				[40.036117, -75.161619],
				[39.981586, -75.149515]
				],
			    {color: 'red', weight: 5}).addTo(map);

// Bind popup to line object
myDataLine.bindPopup("Chestnut Line");
```

#### 6. Add a polygon to the map instance
```js
// create a polygon of Philadelphia metro
var myArea = L.polygon([[40.134261, -75.270050],
			 [40.138132, -74.888837],
			 [39.873212, -74.988837],
			 [39.859046, -75.377775]
			 ],
   			 {color: 'blue', weight: 1}).addTo(map);
   			 
// Bind popup to area object
myArea.bindPopup("Philadelphia metro");
```

#### 7. Create a popup to show the coordinate your click point
```js
// Create an Empty Popup
var popup = L.popup();
// Write function to set Properties of the Popup
function onMapClick(e) {
    popup
        .setLatLng(e.latlng)
        .setContent("You clicked the map at " + e.latlng.toString())
        .openOn(map);
}

// Listen for a click event on the Map element
map.on('click', onMapClick);
```

#### 8. Read the geojson file of blood lead and map
```js
// load GeoJSON from an external file
$.getJSON("blood_lead.geojson",function(data){
    // add GeoJSON layer to the map once the file is loaded
    L.geoJson(data, {
    	onEachFeature: function(feature, layer){
    		layer.bindPopup('Blood lead level: '+feature.properties.perc_5plus);
    	}
    }).addTo(map);
});
```

**If you have difficulty in reading the geojson file**, you can run a localhost to serve your webpage. You can simplely typein `python -m http.server` in your Anaconda prompt, and then open your web browser and typein `localhost:8000`. Make sure your geojson file in the same directory with your `html` file


## Homework
The homework for this week is to redo the homework of last week using HTML/CSS/JavaScript
 - Add markers of cutting points of your routes
 - Add line of your routes
 - Add polygons
