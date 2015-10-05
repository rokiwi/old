---
layout: home
title: "Samoa"
---

<ul>
{% for post in site.categories.samoa %}

<li>
  <a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a>
</li>
  
{% endfor %}
</ul>

<div id="map"></div>


<style>
#map {
  width: 500px;
  height: 200px;
}
</style>

<script src="https://maps.googleapis.com/maps/api/js"></script>
<script>

APIA = "apia";
TAFATAFA = "tafatafa";
LALOMANU = "lalomanu";
FATUOSOFIA = "samatau";

var geocoder;
var map;
var bounds = new google.maps.LatLngBounds();

var volcano = {
 path: 'M26.125 19.97c59.805 21.772 99.325 56.84 127.72 105.31 20.807 35.52 35.428 78.442 46.624 128.282.645 5.295 1.185 10.563 1.685 15.813C154.15 204.955 83.587 166.81 20.56 165.625v.22c58.234 16.936 103.124 50.71 135.19 92.968-29.435-17.817-63.76-23.935-115.03-25.063 88.53 26.684 116.564 46.203 136.935 91.906-50.52-9.608-100.656 16.807-107.28 70 17.742-29.653 41.175-46.612 65.093-48.28 25.746-1.8 32.124 14.687 15.436 37.562l-6.687 8.125c-.162.176-.307.354-.47.53l.063-.03-1.563 1.906-75.938 51.5-.97.685-.78.875-41.063 46.44h24.938l29.374-33.19 76.03-51.56 1.095-.75.875-1.033 49.69-60.467 29.72 15.967 2.968 1.594 3.312-.685 34.656-7.03 1.375-.283 1.22-.655 16.376-8.906h2.25l53.75 57.125.5.53.53.438 113.408 88.907h30.03v-.19L365.782 392.97c-15.184-25.04-5.886-49.94 17.44-54.845 35.786-7.526 64.944-6.61 105.436 11.094-44.382-35.54-97.07-46.684-146.375-30.346 27.234-63.822 87.474-107.53 153.314-132.22v-.718c-68.792 7.528-131.456 37.83-177.844 84.875 11.63-57.223 27.12-105.993 50.28-145.53C396.4 76.86 435.896 41.81 495.597 20.03v-.062H450.19C407.29 43.23 375.5 75.57 351.91 115.842c-12.1 20.65-22.08 43.34-30.53 67.97C332.186 116.106 353.704 53.018 394 19.968h-79.03c-28.243 100.098-41.47 200.18-52.314 300.28-.684-100.097-.42-200.185 12-300.28H183.75C207 88.305 215.438 156.18 217.844 227.186c-12.94-81.71-35.23-150.175-70.313-207.22h-40.28c20.477 19.316 38.15 47.228 52.595 79.844-22.34-32.882-51.07-59.753-88.094-79.843H26.126z',
  fillColor: 'black',
  fillOpacity: 0.8,
  scale: 0.2,
  strokeColor: 'black',
  strokeWeight: 1
};

var goldStar = {
 path: 'M8.698 3.19h-3.3C7.047 1.54 12 2.364 12 2.364c3.302-2.477 4.952-.824 4.952-.824-.825 0-2.476.824-2.476.824 6.603 0 7.43 1.65 7.43 1.65-4.128-.824-7.43 0-7.43 0 4.952 2.478 5.778 5.778 5.778 5.778-3.16-3.16-5.837-3.9-6.917-4.073 1.79 7.81 1.768 9.972 1.345 15.63 3.302 0 4.746 1.65 4.746 1.65H7.048s2.27-1.65 4.745-1.65c0 0 1.906-6.25.365-14.07-.984 2.894-.984 5.814-.984 5.814-1.65-1.65-.824-6.603-.824-6.603-1.65 0-5.778 3.302-5.778 3.302C4.572 7.315 8.7 4.84 8.7 4.84c-4.955.826-6.605 2.476-6.605 2.476 1.65-3.3 6.603-4.126 6.603-4.126z',
  fillColor: 'black',
  fillOpacity: 0.8,
  scale: 2,
  strokeColor: 'black',
  strokeWeight: 1
};

var turtle = {
 path: 'M7.81 8.29c-1.007 1.093-1.275 2.216-1.913 3.325-3.05 2.98-2.756 3.056-3.614 6.882 3.95 2.044 2.56 1.232 7.32 1.354.88.44 1.677.578 2.595-.33-1.055-.19-.77-.684-1.21-1.054 3.866.644 5.785-3.415 8.517-5.892 1.313 1.233 2.382 1.712 4.496 1.825-2.055-2.215-2.807-5.284-1.578-7.923-2.387 1.863-2.7 2.76-3.58 4.327l-1.613-.26c-.334-.22-.33-.58-.146-.806.467-.562-1.553-.074-2.2-.595-.076-.06-.812-.012-1 .82-2.75-.91-4.486-.243-6.075-1.673z',
  fillColor: 'black',
  fillOpacity: 1,
  scale: 2,
  strokeColor: 'black',
  strokeWeight: 2
};

var turtle = {
 path: 'M7.81 8.29c-1.007 1.093-1.275 2.216-1.913 3.325-3.05 2.98-2.756 3.056-3.614 6.882 3.95 2.044 2.56 1.232 7.32 1.354.88.44 1.677.578 2.595-.33-1.055-.19-.77-.684-1.21-1.054 3.866.644 5.785-3.415 8.517-5.892 1.313 1.233 2.382 1.712 4.496 1.825-2.055-2.215-2.807-5.284-1.578-7.923-2.387 1.863-2.7 2.76-3.58 4.327l-1.613-.26c-.334-.22-.33-.58-.146-.806.467-.562-1.553-.074-2.2-.595-.076-.06-.812-.012-1 .82-2.75-.91-4.486-.243-6.075-1.673z',
  fillColor: 'black',
  fillOpacity: 1,
  scale: 2,
  strokeColor: 'black',
  strokeWeight: 2
};

function setMarker(location){ 
  var marker = new google.maps.Marker( 
  { map: map, 
    icon: "r.svg",
    position: location 
  }); 
  setBounds(location);  
  return marker;
}

function getInfoWindow(title,content){

 contentString = '<div id="content">'+
'<div id="siteNotice">'+
'</div>'+
'<h1 id="firstHeading" class="firstHeading">'+ title +'</h1>'+
'<div id="bodyContent">'+ content +
'</div>'+
'</div>';

 return new google.maps.InfoWindow({
   content: contentString
 });
}


function setCenter(location){
  map.setCenter(location);
}

function setBounds(location){
  bounds.extend(location);
  map.setCenter(bounds.getCenter());
  map.fitBounds(bounds);
}

function setMarkerAndInfo(infoWindow){
  return function (location) {
    marker = setMarker(location);
    infoWindow.open(map, marker);
    //marker.addListener('click', function() {
    //   infoWindow.open(map, marker);
    //});
 };
}


function initialize() {
  geocoder = new google.maps.Geocoder();
  var mapCanvas = document.getElementById('map');
  var mapOptions = {
    zoom: 15,
    mapTypeId: google.maps.MapTypeId.ROADMAP
  };
  map = new google.maps.Map(mapCanvas, mapOptions);
  map.set('styles', [ { "featureType": "water", "elementType": "geometry", "stylers": [ { "visibility": "on" }, { "color": "#aee2e0" } ] }, { "featureType": "landscape", "elementType": "geometry.fill", "stylers": [ { "color": "#abce83" } ] }, { "featureType": "poi", "elementType": "geometry.fill", "stylers": [ { "color": "#769E72" } ] }, { "featureType": "poi", "elementType": "labels.text.fill", "stylers": [ { "color": "#7B8758" } ] }, { "featureType": "poi", "elementType": "labels.text.stroke", "stylers": [ { "color": "#EBF4A4" } ] }, { "featureType": "poi.park", "elementType": "geometry", "stylers": [ { "visibility": "simplified" }, { "color": "#8dab68" } ] }, { "featureType": "road", "elementType": "geometry.fill", "stylers": [ { "visibility": "simplified" } ] }, { "featureType": "road", "elementType": "labels.text.fill", "stylers": [ { "color": "#5B5B3F" } ] }, { "featureType": "road", "elementType": "labels.text.stroke", "stylers": [ { "color": "#ABCE83" } ] }, { "featureType": "road", "elementType": "labels.icon", "stylers": [ { "visibility": "off" } ] }, { "featureType": "road.local", "elementType": "geometry", "stylers": [ { "color": "#A4C67D" } ] }, { "featureType": "road.arterial", "elementType": "geometry", "stylers": [ { "color": "#9BBF72" } ] }, { "featureType": "road.highway", "elementType": "geometry", "stylers": [ { "color": "#EBF4A4" } ] }, { "featureType": "transit", "stylers": [ { "visibility": "off" } ] }, { "featureType": "administrative", "elementType": "geometry.stroke", "stylers": [ { "visibility": "on" }, { "color": "#87ae79" } ] }, { "featureType": "administrative", "elementType": "geometry.fill", "stylers": [ { "color": "#7f2200" }, { "visibility": "off" } ] }, { "featureType": "administrative", "elementType": "labels.text.stroke", "stylers": [ { "color": "#ffffff" }, { "visibility": "on" }, { "weight": 4.1 } ] }, { "featureType": "administrative", "elementType": "labels.text.fill", "stylers": [ { "color": "#495421" } ] }, { "featureType": "administrative.neighborhood", "elementType": "labels", "stylers": [ { "visibility": "off" } ] } ]);
  i1 = getInfoWindow("Apia","La capitale");
  geocode(APIA,setMarkerAndInfo(i1));
  i2 = getInfoWindow("maotaomaa","test");
  //alert(i1);
  geocode(TAFATAFA,setMarkerAndInfo(i2));
  i3 = getInfoWindow("Piula","Pool cave");
  geocode("faleapuna",setMarkerAndInfo(i3));
  geocode("falelatai", setBounds);
  geocode("saleapaga", setBounds);
}


function geocode(address,c1){
  geocoder.geocode( {address:address}, 
    function(results, status) { 
      if (status == google.maps.GeocoderStatus.OK) { 
        c1(results[0].geometry.location);
      } 
  });
}


google.maps.event.addDomListener(window, 'load', initialize);

</script>