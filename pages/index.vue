<template>
  <section class="container">
    <header class="header">
      <h1>Code Spots</h1>
      <nav class="navbar">
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
        type="terrain"
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
  mounted() {
    this.getUserLocation();
  },
  data: function() {
    return {
      hereMapId: process.env.hereMapAppId,
      hereMapCode: process.env.hereMapAppCode,
      userLocation: null
    };
  },
  methods: {
    getUserLocation: function() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(position => {
          const lat = position.coords.latitude;
          const lng = position.coords.longitude;
          console.log(lat, lng);
        });
      } else {
        alert("Geolocation is not supported by this browser.");
      }
    }
  }
};
</script>

<style lang="scss">
.container {
  display: flex;
}
.header {
  flex: 1;
}
.header h1 {
  text-align: center;
  padding: 1em;
}
.navbar {
  display: flex;
  flex-direction: column;
}
.map-area {
  flex: 4;
}
</style>
