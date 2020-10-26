# Sitrep

<!DOCTYPE html>
<html>
<head>
<!Include Leaflet CSS file>
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
   integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
   crossorigin=""/>
    
 <!Include Leaflet JavaScript file>
 <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"
   integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA=="
   crossorigin=""></script>

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
    <h3> The International Observatory </h3>
    
<div id="my-map"></div>
<script src="http://localhost:8888/lab/tree/Map/map1.geojson"></script>
    
<!creating my map>
    
    <script> 
   
//create map and set center and zoom level
        
    var mymap = L.map("my-map").setView([51.509, -0.118],0); 
    var attribution ='Map data &copy <a href="https://openstreetmap.org">OpenStreetMap</a> contributors';
    var tileUrl = 'http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png';
    
// basemap layer 
        
    var tiles = L.tileLayer(tileUrl,{ attribution}); 
    tiles.addTo(mymap); 

//adding Json layer (not working )
    
    fetch("http://localhost:8888/lab/tree/Map/map1.geojson")
       .then(function (response){
        return.response.json();  
        })
        .then(function(data){
        L.geoJSON(data).addTo(mymap);
        
    });    
        
//<!Creating my marker>
        
    const Icon = L.icon({
        iconUrl: 'my-icon.png',
        iconSize: [30, 30],
        iconAnchor: [25, 16]
});
    const marker = L.marker([0, 0],{icon: Icon}).addTo(mymap);   
        
//L.marker ([Latitude,longitude.addTo(myMap)])
        
    marker.setLatLng([latitude,longitude]);

        
    </script>
    
</body>
</html>
 
