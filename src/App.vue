<template>
  <div id="container">
   <div id="mapContainer"></div>
 </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";

export default {
 name: "Map",
 data() {
   return{
     center: [0, 0]
   }},
 methods: {
   setupLeafletMap: function () {
    const mapDiv = L.map("mapContainer").setView(this.center, 13);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(mapDiv);
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