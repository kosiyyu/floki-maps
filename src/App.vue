<script setup lang="ts">
import { ref, onMounted } from "vue";
import L from 'leaflet';
import { GeoSearchControl, OpenStreetMapProvider } from 'leaflet-geosearch';
import 'leaflet-fullscreen/dist/Leaflet.fullscreen.js';
import 'leaflet-fullscreen/dist/leaflet.fullscreen.css';
import 'leaflet-geosearch/assets/css/leaflet.css';

let mapContainer = ref(null);
let map: L.Map | unknown = null;


onMounted(() => {
  map = L.map(mapContainer.value as unknown as HTMLElement, {
    fullscreenControl: true,
  }).setView([51.505, -0.09], 3);

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
  }).addTo(map);

  const provider = new OpenStreetMapProvider();

  const searchControl = new GeoSearchControl({
    provider: provider,
  });

  map?.addControl(searchControl);
});

const goFullscreen = () => {
  if(map) {
    map.toggleFullscreen();
  }
};
</script>

<template>
  <div>
    <div id="map-container" ref="mapContainer"></div>
    <button @click="goFullscreen">Go Fullscreen</button>
  </div>
</template>

<style>
#map-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 800px;
  width: 800px;
}
</style>