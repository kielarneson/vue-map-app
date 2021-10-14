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
// /* global MapboxGeocoder */

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

    // Create a default Marker and add it to the map.
    const marker1 = new mapboxgl.Marker().setLngLat([12.554729, 55.70651]).addTo(map);

    // Create a default Marker, colored black, rotated 45 degrees.
    const marker2 = new mapboxgl.Marker({ color: "black", rotation: 45 }).setLngLat([12.65147, 55.608166]).addTo(map);

    console.log(marker1);
    console.log(marker2);
  },
};
</script>
