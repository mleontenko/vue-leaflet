<template>
  <div id="container">
   <div id="mapContainer"></div>
 </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";
import data from "./Historic-Landmarks.json";

export default {
 name: "Map",
 data() {
   return{
     center: [37.7749, -122.4194]
   }},
 methods: {
   setupLeafletMap: function () {
    const mapDiv = L.map("mapContainer").setView(this.center, 13);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(mapDiv);
    //L.geoJSON(data).addTo(mapDiv);
    L.geoJSON(data , {onEachFeature: this.onEachFeature,style: this.styleMap,}).addTo(mapDiv);
   },
   styleMap(feature){
      const year = feature.properties.datelisted
            ? parseInt(feature.properties.datelisted.slice(0, 4))
            : 0;
          const color = year > 2000 ? "red" : "blue";
          return { color: color };
    },
    onEachFeature(feature, layer) {
      if (feature.properties && feature.properties.name) {
        layer.bindPopup(feature.properties.name);
    layer.on('mouseover', () => { layer.openPopup(); });
        layer.on('mouseout', () => { layer.closePopup(); });
      }
   },
 },
 mounted() {
   this.setupLeafletMap();   
 },
};
</script>

<style scoped>
#mapContainer {
 width: 80vw;
 height: 100vh;
}
</style>