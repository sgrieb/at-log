<template>
  <div id="mapContainer"></div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";
import * as esri from 'esri-leaflet';

export default {
  name: "LeafletMap",
  data() {
    return {
      map: null
    };
  },
  mounted() {
    this.map = L.map("mapContainer", { renderer: L.canvas() }).setView([45.526, -122.667], 12);
    L.tileLayer("http://{s}.tile.osm.org/{z}/{x}/{y}.png", {
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(this.map);

    esri.featureLayer({
      url: 'https://services1.arcgis.com/fBc8EJBxQRMcHlei/ArcGIS/rest/services/ANST_Facilities/FeatureServer/8',
      renderer: L.canvas(),
      simplifyFactor: 0.35,
      precision: 5,
    }).addTo(this.map);
  },
  beforeUnmount() {
    if (this.map) {
      this.map.remove();
    }
  }
}
</script>

<style scoped>
#mapContainer {
  width: 100vw;
  height: 100vh;
}
</style>
