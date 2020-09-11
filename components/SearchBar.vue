<template>
  <div class="flex flex-row justify-center" >
    <input
      class="bg-white focus:outline-none focus:shadow-outline border border-gray-300 rounded-l-lg py-2 px-4 w-1/2 appearance-none leading-normal inline-flex mr-0"
      type="text"
      placeholder="Search for any domain"
      v-model="domain"
    />

    <button
      class="bg-black text-white focus:outline-none focus:shadow-outline border border-black rounded-r-lg py-3 px-4 mx-0 inline-flex"
      @click="fetchIpInfo()"
    >
      <img src="../assets/img/icon-arrow.svg" alt="arrow" />
    </button>
  </div>
</template>

<script>
export default {
  name: "SearchBar",
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

<style lang="scss" scoped></style>
