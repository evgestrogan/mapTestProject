<template>
  <l-marker :lat-lng="marker.geometry.coordinates">
    <l-icon
      :icon-size="icon.iconSize"
      :icon-url="icon.iconUrl"
    >
    </l-icon>
    <l-popup>
      <p>
        {{marker.properties.name}}
      </p>
    </l-popup>
  </l-marker>
</template>

<script>
import {
  LMarker,
  LPopup,
  LIcon,
} from 'vue2-leaflet';

export default {
  name: "marker",
  components: {
    LMarker,
    LPopup,
    LIcon,
  },

  props: ['marker'],
  data() {
    return {
      icon: {
        iconUrl: "icon/test.png",
        iconSize: [48, 48],
        iconAnchor: [16, 37]
      },
    }
  },
}
</script>

<style scoped>

</style>