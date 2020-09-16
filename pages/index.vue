<template>
  <div>
    <div id="header" class="">
      <div
        class="container mx-auto px-4 h-32 
      flex flex-col"
      >
        <Title />

        <div class="flex flex-row justify-center">
          <input
            class="bg-white focus:outline-none focus:shadow-outline border border-gray-300 rounded-l-lg py-2 px-4 md:w-1/2 w-full appearance-none leading-normal inline-flex mr-0"
            type="text"
            placeholder="Search for any domain"
            v-model="domain"
            @keyup.enter="fetchIpInfo()"
          />

          <button
            class="bg-black text-white focus:outline-none focus:shadow-outline border border-black rounded-r-lg py-3 px-4 mx-0 inline-flex"
            @click="fetchIpInfo()"
          >
            <img src="../assets/img/icon-arrow.svg" alt="arrow" />
          </button>
        </div>
      </div>
      <Info
        :ipAddress="ipAddress"
        :location="location"
        :timezone="timezone"
        :isp="isp"
      />
    </div>
    <div class="z-0">
      <Map :lat_lng="lat_lng" />
    </div>
  </div>
</template>

<script>
import Title from "../components/Title";
import Info from "../components/Info";
import Map from "../components/Map";
export default {
  components: {
    Title,
    Info,
    Map
  },
  data() {
    return {
      domain: "",
      baseUrl: "https://geo.ipify.org/api/v1",
      lat_lng: [-34.5349754, -58.5224896],
      location: "",
      ipAddress: "",
      isp: "",
      timezone: ""
    };
  },
  methods: {
    isDomainValid(){
      const regex = new RegExp("(?:[a-z0-9](?:[a-z0-9-]{0,61}[a-z0-9])?\.)+[a-z0-9][a-z0-9-]{0,61}[a-z0-9]");

      const isValid = regex.test(this.domain);
      return isValid;
    },
    async fetchIpInfo() {
      if (this.isDomainValid()) {
        
        await this.$axios
          .$get(this.baseUrl, {
            params: {
              apiKey: process.env.API_KEY,
              domain: this.domain
            }
          })
          .then(result => {
            this.location = `${result.location.city}, ${result.location.region}, ${result.location.country}`;
            this.ipAddress = result.ip;
            this.isp = result.isp;
            this.timezone = `UTC ${result.location.timezone}`;
            this.lat_lng = [result.location.lat, result.location.lng];
          })
          .catch(err => {
            alert("Ha ocurrido un error. Revisa si el dominio es valido.")
          })
      }
      else{
        alert('No es un dominio valido.')
      }
    }
  }
};
</script>

<style>
#header {
  background-image: url("../assets/img/pattern-bg.png");
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
