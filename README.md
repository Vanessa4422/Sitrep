<!DOCTYPE html>
<html>
    
<head>
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
   integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
   crossorigin=""/> <!Include Leaflet CSS file>

 <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"
   integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA=="
   crossorigin=""></script> <!Include Leaflet JavaScript file>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js"></script> <!Include geojson file>

<style>
    #my-map {
width:960px;
height:500px;
}
</style>
</head>


<body> 
    <h1>Sitrep Map</h1> 
    <h2> Covid-19 Weekly post reporting </h2> 
    
<div id="my-map"></div>

<!Setting up the map>
<script> 
    var url = 'Map/map1.geojson';  
 
// Setting up my base map
    
    const mymap = L.map("my-map").setView([0, 0], 1);
    const attribution ='Map data &copy <a href="https://openstreetmap.org">OpenStreetMap</a> contributors';
    const tileUrl = 'http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png';
    const tiles = L.tileLayer(tileUrl,{ attribution}).addTo(mymap);
    
// Markers
    
    const  geojsonMarkerOptions = {
        'radius':3,
        'opacity': .5,
        'color': "blue",
        'fillColor':  "blue",
        'fillOpacity': 0.8
};

    function forEachFeature(feature, layer) {
          var popupContent = 
            feature.properties.Country_code;

           if (feature.properties && feature.properties.popupContent) {
                popupContent += feature.properties.popupContent;
            }
                layer.bindPopup(popupContent);
};


 // Defining the empty json layer

    var jlayer = L.geoJSON(null, {
        onEachFeature: forEachFeature, 
        pointToLayer: function (feature, latlng) {
        return L.circleMarker(latlng, geojsonMarkerOptions);
            }});

   
// GeoJSON data 

    var data = {
    "type": "Feature",
      "properties": {
            "Country_code": "ABW",
            "Country": "Aruba",
            "gcode": "Aruba, ARUBA, Nederland"
    },
    "geometry": {
            "type": "Point",
            "coordinates": [-69.9609842, 12.4902998]
    }};
    
    
// Adding json and layer to map; read the data, pass it to the function as data, and add it to the layer. Finally add the layer to the map.

    jlayer.addData(data).addTo(mymap);
    
   
</script>    
</body>
</html>


