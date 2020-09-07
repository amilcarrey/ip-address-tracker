<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title ">
        ip-address-tracker
      </h1>
      <input
        type="text"
        placeholder="Search for any Ip address or domain"
        v-model="domain"
      />
      <input type="button" value="Buscar" @click="fetchIpInfo()" />
      {{ location }}
      
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      domain: "",
      latitude: null,
      logitude: null,
      baseUrl: "https://geo.ipify.org/api/v1",
      location: {}
    };
  },
  methods: {
    async fetchIpInfo() {
      await this.$axios.$get(this.baseUrl, {
        params: {
          apiKey: process.env.API_KEY,
          domain: this.domain
        }
      })
      .then((result) => {
        this.location = result.location;  
      })
      
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
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
