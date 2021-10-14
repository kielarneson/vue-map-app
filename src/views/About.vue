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
    const map = new mapboxgl.Map({
      container: "map",
      style: "mapbox://styles/mapbox/streets-v11",
      center: [12.550343, 55.665957],
      zoom: 8,
    });

    console.log(map);

    this.places.forEach((place) => {
      console.log(place.description, place.lat, place.lng);
      const marker = new mapboxgl.Marker().setLngLat([place.lng, place.lat]).addTo(map);
      console.log(marker);
    });

    // // Create a default Marker and add it to the map.
    // const marker1 = new mapboxgl.Marker().setLngLat([12.554729, 55.70651]).addTo(map);

    // // Create a default Marker, colored black, rotated 45 degrees.
    // const marker2 = new mapboxgl.Marker({ color: "black", rotation: 45 }).setLngLat([12.65147, 55.608166]).addTo(map);
  },
};
</script>
