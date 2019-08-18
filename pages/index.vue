<template>
  <section class="container">
    <header>
      <h1>Code Spots!</h1>
      <nav>
        <ul>
          <li>
            <a href="http://" target="_blank" rel="noopener noreferrer">show something</a>
          </li>
        </ul>
      </nav>
    </header>
    <div class="map-area">
      <HereMap
        :appId="hereMapId"
        :appCode="hereMapCode"
        lat="34.6937"
        lng="135.5022"
        width="100%"
        height="100vh"
      />
    </div>
  </section>
</template>

<script>
import HereMap from "~/components/HereMap.vue";
export default {
  components: {
    HereMap
  },
  data: function() {
    return {
      hereMapId: process.env.hereMapAppId,
      hereMapCode: process.env.hereMapAppCode
    };
  }
};
</script>

<style lang="scss">
.container {
  display: flex;
}
.map-area {
  flex: 2;
}
</style>
