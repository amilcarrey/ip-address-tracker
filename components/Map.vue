<template>
  <div id="map-wrap" style="height: 72.7vh" class="z-0">
    <no-ssr>
      <l-map :zoom="13" :center="lat_lng">
        <l-tile-layer
          url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"
        ></l-tile-layer>
        <l-marker :lat-lng="lat_lng"></l-marker>
      </l-map>
    </no-ssr>
  </div>
</template>

<script>
export default {
  name: "Map",
  props: {
    lat_lng: {
      type: Array,
      default: [-34.5349754, -58.5224896]
    }
  }
};
</script>

<style lang="scss" scoped></style>
