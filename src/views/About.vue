<template>
  <div class="about">
    <button id="find-me">Show my location</button>
    <br />
    <p id="status"></p>
    <a id="map-link" target="_blank"></a>
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
/* global mapboxgl, MapboxDirections */

export default {
  data: function () {
    return {
      places: [
        { lat: 41.8789123, lng: -87.6362009, description: "Sears Tower" },
        { lat: 41.8987503, lng: -87.6230425, description: "Hancock Building" },
      ],
    };
  },
  mounted: function () {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_API_KEY;
    const map = new mapboxgl.Map({
      container: "map",
      style: "mapbox://styles/mapbox/streets-v11",
      center: [-87.6249131, 41.8762194],
      zoom: 12,
    });

    console.log(map);

    this.places.forEach((place) => {
      console.log(place.description, place.lat, place.lng);
      const marker = new mapboxgl.Marker().setLngLat([place.lng, place.lat]).addTo(map);
      console.log(marker);
    });

    var directions = new MapboxDirections({
      accessToken: mapboxgl.accessToken,
    });

    map.addControl(directions, "top-left");

    map.on("load", function () {
      directions.setOrigin("Soldier Field, Chicago, IL"); // can be address in form setOrigin("12, Elm Street, NY")
      // directions.setDestinaion([]); // can be address
    });
    // // Create a default Marker and add it to the map.
    // const marker1 = new mapboxgl.Marker().setLngLat([12.554729, 55.70651]).addTo(map);

    // // Create a default Marker, colored black, rotated 45 degrees.
    // const marker2 = new mapboxgl.Marker({ color: "black", rotation: 45 }).setLngLat([12.65147, 55.608166]).addTo(map);
  },
};
</script>
