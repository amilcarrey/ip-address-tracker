<template>
    <div class="container ">
      <div class="search-bar block ">
        <input
          class="bg-white focus:outline-none focus:shadow-outline border border-gray-300 rounded-lg py-2 px-4 block w-1/2 appearance-none leading-normal inline-flex"
          type="text"
          placeholder="Search for any Ip address or domain"
          v-model="domain"
        />
        <input class="inline-flex"type="button" value="Buscar" @click="fetchIpInfo()" />
      </div>
      <div class="results block">
        {{ result }}
      </div>
    </div>

</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>

</style>