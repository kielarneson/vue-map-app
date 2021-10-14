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
/* global mapboxSdk */

export default {
  data: function () {
    return {
      places: [
        { lat: -25.363, lng: 131.044, description: "A place in Australia" },
        { lat: -33.8675, lng: 151.207, description: "The main city!" },
      ],
    };
  },
  mounted: function () {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_API_KEY;
    const mapboxClient = mapboxSdk({ accessToken: mapboxgl.accessToken });
    mapboxClient.geocoding
      .forwardGeocode({
        query: "Wellington, New Zealand",
        autocomplete: false,
        limit: 1,
      })
      .send()
      .then((response) => {
        if (!response || !response.body || !response.body.features || !response.body.features.length) {
          console.error("Invalid response:");
          console.error(response);
          return;
        }
        const feature = response.body.features[0];

        const map = new mapboxgl.Map({
          container: "map",
          style: "mapbox://styles/mapbox/streets-v11",
          center: feature.center,
          zoom: 10,
        });

        // Create a marker and add it to the map.
        new mapboxgl.Marker().setLngLat(feature.center).addTo(map);
      });
  },
};
</script>
