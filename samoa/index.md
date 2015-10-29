---
layout: home
---

<div>

<div id="post"></div>

<div id="map"></div>

<p>
  <a href="JavaScript:showAllIcons()">Toutes les icônes,</a>
  <a href="JavaScript:setBounds(samoa)"> Samoa,</a>
  <a href="JavaScript:setBounds(savaii)"> Savai'i,</a>
  <a href="JavaScript:setBounds(upolu)"> Upolu,</a>
  <a href="JavaScript:setBounds(manono)"> Manono</a>
</p>

<style>
#map {
  width: 90vw; 
  height: 60vw; 
}
</style>

<script src="https://maps.googleapis.com/maps/api/js"></script>

<script>
var map;
var markers = new Array();
var markersCl = new Array();

var samoa = [
  new google.maps.LatLng(-13.499144,-172.78738),
  new google.maps.LatLng(-13.451613, -172.33061),
  new google.maps.LatLng(-13.8756895, -171.60178),
  new google.maps.LatLng(-14.037134, -171.67784)
];

var savaii = [
  new google.maps.LatLng(-13.499144,-172.78738),
  new google.maps.LatLng(-13.451613, -172.33061),
  new google.maps.LatLng(-13.66891, -172.17941),
  new google.maps.LatLng(-13.801262, -172.52443)
];

var upolu = [
  new google.maps.LatLng(-13.83045,-172.0081),
  new google.maps.LatLng(-13.8756895, -171.60178),
  new google.maps.LatLng(-14.037134, -171.67784)
];

var manono = [
  new google.maps.LatLng(-13.853478,-172.11687),
  new google.maps.LatLng(-13.83045, -172.0081),
  new google.maps.LatLng(-13.753836,-172.11687)
];

function setPost(code) {
  $('#post').load('/samoa/2015/08/' + code + '/', function() {
    $('#post').get(0).scrollIntoView();
  });
}

function setBounds(bounds){
  var bs = new google.maps.LatLngBounds();
  bounds.forEach(function(a) { 
    bs.extend(a);
  });
  map.fitBounds(bs);
}

function addListener(i) {
  google.maps.event.addListener(i, 'click', 
      function() { 
       nextIcon();
       setPost(i.co); 
       
      }
    ); 
  }

function setMarkerFromLocation(x,y,id,icon){
  var location = new google.maps.LatLng(x,y);
  var m;

  var image = {
    url: "/samoa/icon/" + icon + ".svg",
    size: new google.maps.Size(50, 50),
    origin: new google.maps.Point(0, 0),
    anchor: new google.maps.Point(25, 25),
    scaledSize: new google.maps.Size(25, 25)
  };

  m = new google.maps.Marker( 
  { icon: image,
    position: location,
    co: id
  }); 
  markers.push(m);
  addListener(m);
}

function nextIcon() {
  if(markers.length > 0){
    if(markersCl.length > 0){
      var prev = markersCl[markersCl.length - 1];
      prev.setMap(null);
    }
    var mar = markers.shift();
    markersCl.push(mar);
    mar.setMap(map);
  }else{
    showAllIcons();
  }
}

function showAllIcons() {
  markersCl = markers.concat(markersCl);
  markers = new Array();

  $.each( markersCl, function( key, value ) {
    value.setMap(map);
  });


}

function setStyles(map){
  map.set('styles', [ { "featureType": "water", "elementType": "geometry", "stylers": [ { "visibility": "on" }, { "color": "#aee2e0" } ] }, { "featureType": "landscape", "elementType": "geometry.fill", "stylers": [ { "color": "#abce83" } ] }, { "featureType": "poi", "elementType": "geometry.fill", "stylers": [ { "color": "#769E72" } ] }, { "featureType": "poi", "elementType": "labels.text.fill", "stylers": [ { "color": "#7B8758" } ] }, { "featureType": "poi", "elementType": "labels.text.stroke", "stylers": [ { "color": "#EBF4A4" } ] }, { "featureType": "poi.park", "elementType": "geometry", "stylers": [ { "visibility": "simplified" }, { "color": "#8dab68" } ] }, { "featureType": "road", "elementType": "geometry.fill", "stylers": [ { "visibility": "simplified" } ] }, { "featureType": "road", "elementType": "labels.text.fill", "stylers": [ { "color": "#5B5B3F" } ] }, { "featureType": "road", "elementType": "labels.text.stroke", "stylers": [ { "color": "#ABCE83" } ] }, { "featureType": "road", "elementType": "labels.icon", "stylers": [ { "visibility": "off" } ] }, { "featureType": "road.local", "elementType": "geometry", "stylers": [ { "color": "#A4C67D" } ] }, { "featureType": "road.arterial", "elementType": "geometry", "stylers": [ { "color": "#9BBF72" } ] }, { "featureType": "road.highway", "elementType": "geometry", "stylers": [ { "color": "#EBF4A4" } ] }, { "featureType": "transit", "stylers": [ { "visibility": "off" } ] }, { "featureType": "administrative", "elementType": "geometry.stroke", "stylers": [ { "visibility": "on" }, { "color": "#87ae79" } ] }, { "featureType": "administrative", "elementType": "geometry.fill", "stylers": [ { "color": "#7f2200" }, { "visibility": "off" } ] }, { "featureType": "administrative", "elementType": "labels.text.stroke", "stylers": [ { "color": "#ffffff" }, { "visibility": "on" }, { "weight": 4.1 } ] }, { "featureType": "administrative", "elementType": "labels.text.fill", "stylers": [ { "color": "#495421" } ] }, { "featureType": "administrative.neighborhood", "elementType": "labels", "stylers": [ { "visibility": "off" } ] } ]);
}

function initialize() {
  
  $('#post').load('/samoa/2015/08/story/');
  var mapCanvas = document.getElementById('map');
  var mapOptions = {
    zoom: 10,
    mapTypeId: google.maps.MapTypeId.ROADMAP
  };
  map = new google.maps.Map(mapCanvas, mapOptions);
  setStyles(map);

  setMarkerFromLocation(-13.753836,-172.11687,"ferry","ferry");
  setMarkerFromLocation(-13.613283,-172.20215, "joelan","fale");
  setMarkerFromLocation(-13.748744,-172.22913,"salelonga", "market");
  setMarkerFromLocation(-13.66891,-172.17941,"bus","bus");

  setMarkerFromLocation(-13.451613,-172.33061, "lava-fields", "church");
  setMarkerFromLocation(-13.536176,-172.39386, "crater-man","crater");
  setMarkerFromLocation(-13.499144,-172.78738, "falealupo","snorkel");
  setMarkerFromLocation(-13.745346,-172.3137, "afa-aau-waterfall","waterfall");
  setMarkerFromLocation(-13.708181,-172.60092, "satuiatua","fale");
  setMarkerFromLocation(-13.801262,-172.52443,"blow-hole","blow-hole");
  setMarkerFromLocation(-14.037134,-171.67784, "maota-o-maa","fale");
  setMarkerFromLocation(-14.0157,-171.7358,"coastal-walk", "hiker");
  setMarkerFromLocation(-13.834241,-171.77185, "apia", "market");
  setMarkerFromLocation(-13.8756895,-171.60178, "piula-cave", "church");
  setMarkerFromLocation(-13.853478,-172.11687, "manono", "fale");
  setMarkerFromLocation(-13.83045,-172.0081, "plane", "plane");

  setBounds(samoa);
  nextIcon();
}


google.maps.event.addDomListener(window, 'load', initialize);

</script>



