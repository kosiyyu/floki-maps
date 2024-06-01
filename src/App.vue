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
  <div id="outher-container">
    <div id="title">
      <span class="rainbow" v-for="(letter, index) in 'FlokiMaps'.split('')" :key="index">{{ letter }}</span>
    </div>
    <button id="button" @click="goFullscreen">Enter maps</button>
    </div>
    <div id="map-container" ref="mapContainer"></div>
</template>

<style>
@font-face {
  font-family: 'Abril Fatface';
  src: url('./assets/AbrilFatface-Regular.ttf') format('truetype');
}

#map-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 0px;
  width: 0px;
}

#outher-container {
  background-color: #052e16;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#title {
  font-family: 'Abril Fatface', sans-serif;
  color: white;
  padding: 10px 20px;
  border: none;
  font-size: 198px;
}

.rainbow:nth-child(1) { color: red; }
.rainbow:nth-child(2) { color: orange; }
.rainbow:nth-child(3) { color: yellow; }
.rainbow:nth-child(4) { color: green; }
.rainbow:nth-child(5) { color: blue; }
.rainbow:nth-child(6) { color: indigo; }
.rainbow:nth-child(7) { color: violet; }
.rainbow:nth-child(8) { color: red; }
.rainbow:nth-child(9) { color: orange; }

#button {
  margin-top: 20px;
  background-color: black;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  font-size: 24px;
  white-space: nowrap;
  border-top-left-radius: 50px;
  border-bottom-left-radius: 50px;
  border-top-right-radius: 50px;
  border-bottom-right-radius: 50px;
  transition: box-shadow;
}

#button:hover {
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
}
</style>