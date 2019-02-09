<template>
  <section class="container">
    <h1>Code Spots!</h1>
    <HereMap
      :appId="hereMapId"
      :appCode="hereMapCode"
      lat="37.7397"
      lng="-121.4252"
      width="100%"
      height="835px"
    />
  </section>
</template>

<script>
import HereMap from "~/components/HereMap.vue";
export default {
  components: {
    HereMap
  },
  data: () => ({
    hereMapId: process.env.hereMapAppId,
    hereMapCode: process.env.hereMapAppCode
  }),
  head() {
    return {
      script: [
        {
          src: "https://js.api.here.com/v3/3.0/mapsjs-core.js",
          body: true,
          defer: true
        },
        {
          src: "https://js.api.here.com/v3/3.0/mapsjs-service.js",
          body: true,
          defer: true
        }
      ]
    };
  }
};
</script>

<style>
</style>
