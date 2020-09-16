<template>
    <div class="block mt-16 ">
          <div class="block md:flex md:justify-around rounded-lg bg-gray-100 py-4 md:pd-8">
            <div class="px-6 py-2 md:py-4 md:border-r-2 w-full md:w-1/4">
              <span class="block text-xs font-medium text-gray-600">IP ADDRESS</span>
              <span class="text-2xl font-bold">{{ ipAddress }}</span>
            </div>
            <div class="px-6 py-2 md:py-4 md:border-r-2 w-full md:w-1/4">
              <span class="block text-xs font-medium text-gray-600">LOCATION</span>
              <span class="text-lg font-bold">{{ location }}</span>
            </div>
            <div class="px-6 py-2 md:py-4 md:border-r-2 w-full md:w-1/4">
              <span class="block text-xs font-medium text-gray-600">TIMEZONE</span>
              <span class="text-2xl font-bold ">{{ timezone }}</span>
            </div>
            <div class="px-6 py-2 md:py-4 w-full md:w-1/4">
              <span class="block text-xs font-medium text-gray-600 ">ISP</span>
              <span class="text-2xl font-bold">{{ isp }}</span>
            </div>
          </div>
        </div>
</template>

<script>
    export default {
        name: "Info",
        props: {
            ipAddress: {
                type: String,
                default: "" 
            },
            location: {
                type: String,
                default: "" 
            },
            timezone: {
                type: String,
                default: "" 
            },
            isp: {
                type: String,
                default: "" 
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>