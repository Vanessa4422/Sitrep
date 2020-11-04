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
h1 {text-align: center;} h1 {color: #012169;}
h2 {text-align: center;} h2 {color: #012169;}
h3 {text-align: center;} h3 {color: #012169;}
    
    #my-map {
width:960px;
height:500px;
display: block;
margin-left: auto;
margin-right: auto;
width: 75%;
}


/* Style the header with a grey background and some padding */
.header {
  overflow: hidden;
  background-color: #f1f1f1;
  padding: 30px 10px;
}

/* Style the header links */
.header a {
  float: left;
  color: #012169;
  text-align: left;
  padding: 12px;
  text-decoration: none;
  font-size: 20px;
  line-height: 25px;
  border-radius: 4px;
  text-align: center;
}

/* Style the logo link (notice that we set the same value of line-height and font-size to prevent the header to increase when the font gets bigger */
.header a.logo {
  font-size: 20px;
  font-weight: bold;
}

/* Change the background color on mouse-over */
.header a:hover {
  background-color: #0000;
  color: black;
}

/* Style the active/current link*/
.header a.active {
  background-color: #012169;
  color: white;
}

/* Float the link section to the right */
.header-right {
  float: right;
}

/* Add media queries for responsiveness - when the screen is 500px wide or less, stack the links on top of each other */
@media screen and (max-width: 500px) {
  .header a {
    float: none;
    display: block;
    text-align: left;
  }
  .header-right {
    float: none;
  }
}    
    
    </style>
</head>


<body> 
    <div class="header">
  <a href="#default" class="logo">Foreign Commonweath and Development Office </a>      
  <div class="header-right">
    <a class="active" href="#home">Home</a>
    <a href="#contact">Contact</a>
    <a href="#about">About</a>
  </div>
</div>
    
    
    <body bgcolor="#FFFFFF">
    <h1>Sitrep Map</h1> 
    <h3> Covid-19 Weekly post reporting </h3> 
    
<div id="my-map"></div>

<!Setting up the map>
<script> 
    var url = 'Map/map1.geojson';  
 
// Setting up my base map
    
    const mymap = L.map("my-map").setView([51.5074, 0.1278], 2);
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
    
    
// Adding json to layer and adding to map

    jlayer.addData(data).addTo(mymap);
    
   
</script>    
</body>
</html>


