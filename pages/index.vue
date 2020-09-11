<template>
  <div>
    <div id="header">
      <div
        class="container mx-auto px-4 h-64 
      flex flex-col "
      >
        <Title />

        <SearchBar />

        <div class="block">
          {{ result }}
        </div>
      </div>
    </div>
    <!-- <Map lat_lng="lat_lng"/> -->
    <div id="map-wrap" style="height: 72.7vh">
      <no-ssr>
        <l-map :zoom="13" :center="lat_lng">
          <l-tile-layer
            url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"
          ></l-tile-layer>
          <l-marker :lat-lng="lat_lng"></l-marker>
        </l-map>
      </no-ssr>
    </div>
  </div>
</template>

<script>
import Title from "../components/Title";
import SearchBar from "../components/SearchBar";
import Map from "../components/Map";
export default {
  components: {
    Title,
    SearchBar,
    Map
  },
  data() {
    return {
      domain: "",
      baseUrl: "https://geo.ipify.org/api/v1",
      location: {},
      lat_lng: [-34.5349754, -58.5224896],
      result: {}
    };
  },
  methods: {
    async fetchIpInfo() {
      await this.$axios
        .$get(this.baseUrl, {
          params: {
            apiKey: process.env.API_KEY,
            domain: this.domain
          }
        })
        .then(result => {
          this.location = result.location;
          this.result = result;
          this.lat_lng = [result.location.lat, result.location.lng];
        });
    }
  }
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
#header {
  background-image: url("../assets/img/pattern-bg.png");
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
