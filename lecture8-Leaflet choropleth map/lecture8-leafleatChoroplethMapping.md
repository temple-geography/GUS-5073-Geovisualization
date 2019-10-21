# Week 8. Introduction of Choropleth Mapping in JavaScript
This week we are going to learn how to use Leaflet to create dynamic choropleth map. We will also add different map elements to the map. Those elements include Map, title, legend, data source, scale, etc. We will also add interactions to the choropleth map. 

### 1. Introduction of HTML/JavaScript/CSS
Recap of last week create markers, lines, and polygonsChoropleth Mapping

Most websites are based on three core technologies: HTML, CSS, and JavaScript. HTML stands for HyperText Markup Language; it is the lingua franca of web documents. It allows you to write structured content in a way that web browsers will understand. CSS stands for Cascading Style Sheet and provides a means to style a website using structure written into the document using HTML. Javascript is the web's preferred programming language and is supported by all browsers without additional plugins. We'll be using it to build interactive visualizations and web pages. JavaScript is extended by a huge number of libraries; we'll be doing our data visualization work in Leaflet.js, Mapbox.js, etc. 

This week we are going to create dynamic geoviz with interactions.
- Load GeoJson file in Leaflet
- reate choropleth map based on the GeoJson file
- Create interaction for each feature in the GeoJson file
- Add Legend for the map
- Add other map elements, scale, data sources, map title, etc. 

### 2. Load geojson file and create choropleth map
Last week we talked about creating markers, lines, polygons to the map instance using Leaflet.js. This week let's load `geojson` file and create choropleth map using leaflet. Our previous code looks like this, 
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Leaflet Map</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.3/dist/leaflet.css"/>
    <style>

    </style>
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

        // add point marker
        var myDataPoint = L.marker([39.981192, -75.155399]).addTo(map);
        myDataPoint.bindPopup("This is Temple University.");
        myDataPoint.bindPopup("<h3>Temple University</h3><p>Philadelphia, PA<br>Information about Temple University.</p>");
        
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

        // create a polygon of Philadelphia metro
        var myArea = L.polygon([[40.134261, -75.270050],
                                 [40.138132, -74.888837],
                                 [39.873212, -74.988837],
                                 [39.859046, -75.377775]
                                 ],
                     {color: 'blue', weight: 1}).addTo(map);

        // Bind popup to area object
        myArea.bindPopup("Philadelphia metro");

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

        // load GeoJSON from an external file
        $.getJSON("blood_lead.geojson",function(data){
            // add GeoJSON layer to the map once the file is loaded
            L.geoJson(data, {
                
            }).addTo(map);
        });
    </script>
</body>
</html>
```
We just load the GeoJson file using the function of `$.getJSON`. We actually just load the file and don't have any operation yet. So, let assign each census tract to a different color first. 


**Add css statement** to your division between `style`,

```css
    html { height:100%;}
    body {
        height:100%;
        padding: 0;
        margin: 0;
    }

    #map {
        width: 100%;
        margin: 0 auto;
        height: 95%;
    }
```


#### Assign different colors to different census tracts based on their data

Let just set the `style` parameter to your `L.geoJson` function. The attribute of `style` is set to a function, which will return different values based on the attribute of each feature. Using the following statement to replace your previous `$.getJSON` statement.

```js
var neighborhoodsLayer = null;
$.getJSON("data/blood_lead.geojson",function(data){
    neighborhoodsLayer = L.geoJson(data, {
        style: styleFunc,
        onEachFeature: function(feature, layer){
            layer.bindPopup('Blood lead level: '+feature.properties.perc_5plus);
        }
    }).addTo(map);
});

```

We need further to define the function of styleFunc. Put the following statement behind your above `$.getJSON` function. This function will return different colors based on the `perc_5plus` to fill each census tract. 

```js
// Set style function that sets fill color property equal to blood lead
function styleFunc(feature) {
    return {
        fillColor: setColorFunc(feature.properties.perc_5plus),
        fillOpacity: 0.9,
        weight: 1,
        opacity: 1,
        color: '#ffffff',
        dashArray: '3'
    };
}

```

In the function, we set the `fillColor` as a dependent variable of the blood level, we need to define the function of `setColorFunc`

```js
// Set function for color ramp, you can use a better palette
function setColorFunc(density){
    return density > 15 ? '#800000' :
           density > 10 ? '#A0522D' :
           density > 5 ? '#DAA520' :
           density > 0 ? '#FFF8DC' :
                         '#BFBCBB';
};

```

Then you can refresh your webpage and you will be able to see your choropleth map.

**Note** 
I know you may here ask, how can I know which function should I use. While, my answer is you will know when you read numbers of tutorials and create your own geoviz. It takes time, and you can read the document of Leaflet or other libraries to make the process shorter, here is the link of Leaflet doc ([Link](https://leafletjs.com/reference-1.5.0.html))


### 3. Create interactions to your choropleth Map
We just create our choropleth map using HTML/JavaScript. We can use the same method for other types of datasets. We can create user interactions to make the geoviz looks better. Let's do it. 

In our current code, we use the following statement to show the attribute when we click the census tract. 
```js
onEachFeature: function(feature, layer){
    layer.bindPopup('Blood lead level: '+feature.properties.perc_5plus);
}
```

Let's replace the statement by `onEachFeature: onEachFeatureFunc`. We here use a function to set the attribute of `onEachFeature`. `onEachFeatureFunc` is the function name, you can use other name as well. This is similar with our previous `style` paramter. So, we need to define and implement the function. Here is the code to implement the function.
```js
// Now we’ll use the onEachFeature option to add the listeners on our state layers:
function onEachFeatureFunc(feature, layer){
    layer.on({
        mouseover: highlightFeature,
        mouseout: resetHighlight,
        click: zoomFeature
    });
    layer.bindPopup('Blood lead level: '+feature.properties.perc_5plus);
}
```
In the above statement, we add one more line in the function, `layer.on({...})`. In this line, we add interactions for user mouseover, mouseout, and click over the census tract. For example, when users have mouse over one census tract, then we will call the function of `highlightFeature`, which is a function we will implement shortly. It is the same for mouseout, and click. 

Let's then implement the functions of `highlightFeature`, `resetHighlight`, and `click`. 

#### For highlightFeature
```js
function highlightFeature(e){
    var layer = e.target;

    layer.setStyle({
        weight: 5,
        color: '#666',
        dashArray: '',
        fillOpacity: 0.7
    });
    // for different web browsers
    if (!L.Browser.ie && !L.Browser.opera && !L.Browser.edge) {
        layer.bringToFront();
    }
}
```

#### For resetHighlight
```js
// Define what happens on mouseout:
function resetHighlight(e) {
    neighborhoodsLayer.resetStyle(e.target);
}  
```

#### For zoomFeature
```js
// As an additional touch, let’s define a click listener that zooms to the state: 
function zoomFeature(e){
    console.log(e.target.getBounds());
    map.fitBounds(e.target.getBounds().pad(1.5));
}
```

### 4. Add scale to the map
It is super simple to add a scale to the map. In this example, we just add one scale bar at the bottomleft, you can add it to other places as well. 
```js
// Add Scale Bar to Map
L.control.scale({position: 'bottomleft'}).addTo(map);

```

### 5. Add legend to the map
A complete map usually need a legend. Therefore, we need to create a legend for the created choropleth map. Make sure the lengend has the same color scheme with your main map. 

```js
// Create Leaflet Control Object for Legend
var legend = L.control({position: 'bottomright'});

// Function that runs when legend is added to map
legend.onAdd = function (map) {
    // Create Div Element and Populate it with HTML
    var div = L.DomUtil.create('div', 'legend');            
    div.innerHTML += '<b>Blood lead level</b><br />';
    div.innerHTML += 'by census tract<br />';
    div.innerHTML += '<br>';
    div.innerHTML += '<i style="background: #800000"></i><p>15+</p>';
    div.innerHTML += '<i style="background: #A0522D"></i><p>10-15</p>';
    div.innerHTML += '<i style="background: #DAA520"></i><p>5-10</p>';
    div.innerHTML += '<i style="background: #DEB887"></i><p>0-5</p>';
    div.innerHTML += '<hr>';
    div.innerHTML += '<i style="background: #BFBCBB"></i><p>No Data</p>';
    
    // Return the Legend div containing the HTML content
    return div;
};

// Add Legend to Map
legend.addTo(map);

```
If you read carefully of the above statement, you may realize we actually using JavaScript to create a HTML `div` and change the properties of `div`. This is what we usually do using JavaScript to manipuate the HTML tags and create dynamic and interactive online geovisualization. 

After you done this, you are technically done for this tutorial. Please just refresh your webpage, then you will send a dynamic and interactive online geovisualization. 


### 6. Organize your JavaScript code and CSS code
This part is just for good practice. You current code can create the interactive geovisualization as you want. However, if you go over your whole code one more time, you may see, you code is mixed with HTML, JavaScript, or CSS code. Just think about if you write a much more complicated webpage or website, it is probably not a good idea to put all of these in one document. So, a good practice is to seperate your JavaScript, HTML, CSS code into different documents. 

You can just create new folders of JS, CSS, or even folders for other documents in your directory. And then you can cut your JavaScript code, which is between your two `script` div, and paste, save it as a new JavaScript code. Then you use  `<script src="JS/your_js_name.js"></script>` to replace your `script` div. 


## Homework 
1. Finish the tutorial and create a interactive and dynamic geoviz. 

2. Using a the field of "num_bll_5p", different color scheme, and different scale of legend

3. Upload your `.html` file to the Canvas. 


