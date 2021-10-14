<template>
  <div class="about">
    <div id="map"></div>
  </div>
</template>

<style scoped>
body {
  margin: 0;
  padding: 0;
}
#map {
  height: 75vh;
}
</style>

<script>
/* global mapboxgl */

export default {
  mounted: function () {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_API_KEY;
    const map = new mapboxgl.Map({
      container: "map", // container ID
      style: "mapbox://styles/mapbox/streets-v11", // style URL
      center: [-74.5, 40], // starting position [lng, lat]
      zoom: 9, // starting zoom
    });
    console.log(map);
  },
};
</script>
