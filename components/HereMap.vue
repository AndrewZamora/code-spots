<template>
  <div class="here-map">
    <button @click="addMarkers">Add markers</button>
    <div ref="map" :style="{ width: width, height: height }"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      map: {},
      platform: {}
    };
  },
  props: {
    appId: String,
    appCode: String,
    lat: String,
    lng: String,
    width: String,
    height: String,
    type: String
  },
  created() {
    if (process.browser) {
      this.platform = new H.service.Platform({
        app_id: this.appId,
        app_code: this.appCode
      });
    }
  },
  mounted() {
    this.map = new H.Map(
      this.$refs.map,
      this.platform.createDefaultLayers()[this.type].map,
      {
        zoom: 10,
        center: { lng: this.lng, lat: this.lat }
      }
    );
    // Enable the event system on the map instance:
    var mapEvents = new H.mapevents.MapEvents(this.map);
    // Instantiate the default behavior, providing the mapEvents object:
    var behavior = new H.mapevents.Behavior(mapEvents);
  },
  methods: {
    addMarkers: function() {
      //    // Define a variable holding SVG mark-up that defines an icon image:
      // var svgMarkup =
      //   '<svg width="24" height="24" ' +
      //   'xmlns="http://www.w3.org/2000/svg">' +
      //   '<rect stroke="white" fill="#1b468d" x="1" y="1" width="22" ' +
      //   'height="22" /><text x="12" y="18" font-size="12pt" ' +
      //   'font-family="Arial" font-weight="bold" text-anchor="middle" ' +
      //   'fill="white">H</text></svg>';

      // // Create an icon, an object holding the latitude and longitude, and a marker:
      // var icon = new H.map.Icon(svgMarkup),
      //   coords = { lat: 52.53075, lng: 13.3851 },
      //   marker = new H.map.Marker(coords, { icon: icon });

      // // Add the marker to the map and center the map at the location of the marker:
      // this.map.addObject(marker);
      // this.map.setCenter(coords);
      // Add event listeners:
      const that = this;
      this.map.addEventListener("tap", function(evt) {
        var coord = that.map.screenToGeo(
          evt.currentPointer.viewportX,
          evt.currentPointer.viewportY
        );
        console.log(`LAT:${coord.lat}`, `LNG:${coord.lng}`);
      });
    }
  }
};
</script>

<style scoped>
.here-map {
  background: #cccccc;
}
</style>
