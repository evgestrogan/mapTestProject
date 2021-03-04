<template>

  <div class="home" style="height: 100%">

    <v-navigation-drawer app apppermanent expand-on-hover width="400">
      <v-list>
        <v-list-group multiple v-for="item in items" :key="item.title" :prepend-icon="item.action" no-action>
          <template v-slot:activator>
            <v-list-item-content>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item-content>
          </template>

          <v-list-item v-for="child in item.items" :key="child.title" @click="child.active = !child.active">
              <v-list-item-action>
                <v-icon v-if="!child.active" color="grey lighten-1">mdi-star-outline</v-icon>
                <v-icon v-else color="yellow darken-3" >mdi-star</v-icon>
              </v-list-item-action>

              <v-list-item-content>
                <v-list-item-title>{{child.title}}</v-list-item-title>
              </v-list-item-content>
          </v-list-item>
        </v-list-group>
      </v-list>
    </v-navigation-drawer>

    <l-map
      v-if="showMap"
      :zoom="zoom"
      :center="center"
      :options="mapOptions"
      style="height: 92.5%; width: 92.5%; position: fixed"
    >
      <l-tile-layer
        :url="url"
        :attribution="attribution"
      />
    </l-map>

    <v-navigation-drawer app apppermanent expand-on-hover right width="400">
    </v-navigation-drawer>

  </div>
</template>

<script>
import { latLng } from 'leaflet';
import {
  LMap,
  LTileLayer,
  LMarker,
  LPopup,
  LTooltip,
  LFeatureGroup,
} from 'vue2-leaflet';

export default {
  name: "Home",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
    LTooltip,
    LFeatureGroup,
  },
  data() {
    return {
      zoom: 7.2,
      center: latLng(53.514797, 28.619385),
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      mapOptions: {
        zoomSnap: 0.1,
        zoomDelta: 0.1,
      },
      showMap: true,

      items: [
        {
          action: 'mdi-ticket',
          items: [{ title: 'List Item', 'active': false }],
          title: 'Attractions',
        },
        {
          action: 'mdi-silverware-fork-knife',
          items: [
            { title: 'Breakfast & brunch', 'active': true },
            { title: 'New American', 'active': false },
            { title: 'Sushi', 'active': true },
          ],
          title: 'Dining',
        },
        {
          action: 'mdi-school',
          items: [{ title: 'List Item', 'active': false }],
          title: 'Education',
        },
        {
          action: 'mdi-run',
          items: [{ title: 'List Item', 'active': false }],
          title: 'Family',
        },
        {
          action: 'mdi-bottle-tonic-plus',
          items: [{ title: 'List Item', 'active': false }],
          title: 'Health',
        },
        {
          action: 'mdi-content-cut',
          items: [{ title: 'List Item', 'active': false }],
          title: 'Office',
        },
        {
          action: 'mdi-tag',
          items: [{ title: 'List Item', 'active': false }],
          title: 'Promotions',
        },
      ],
    };
  },
  methods: {
  },
};
</script>
