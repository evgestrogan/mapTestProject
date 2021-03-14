<template>

  <div class="mappage" style="height: 100%">

    <v-navigation-drawer app apppermanent expand-on-hover mini-variant-width="5" width="50%">
      <v-row style="height: 100%;overflow: hidden">
        <v-col style="overflow-y: scroll; height: 100%">
          <v-card-text style="overflow: auto">
            <v-treeview
              v-model="selection"
              :items="items"
              selected-color="green darken-4"
              open-on-click
              selectable
              return-object
              expand-icon="mdi-chevron-down"
              on-icon="mdi-bookmark"
              off-icon="mdi-bookmark-outline"
              indeterminate-icon="mdi-bookmark-minus"
            >
            </v-treeview>
          </v-card-text>
        </v-col>

        <v-divider vertical></v-divider>

        <v-col cols="12" md="6">
          <v-card-text class="sticky">
            <div v-if="selection.length === 0" key="title" class="title font-weight-light grey--text pa-4 text-center">
              Select your favorite breweries
            </div>
            <div v-else key="title" class="title font-weight-light grey--text pa-4 text-center">
              Your favorite breweries
            </div>
            <v-scroll-x-transition group hide-on-leave>
              <v-chip
                v-for="(select, i) in selection"
                :key="i"
                color="grey"
                dark
                class="ma-1"
                close
                @click:close="selection.splice(select, 1)"
              >
                {{ select.name }}
              </v-chip>
            </v-scroll-x-transition>
          </v-card-text>
        </v-col>
      </v-row>
    </v-navigation-drawer>

    <l-map
      v-if="showMap"
      :zoom="zoom"
      :center="center"
      :options="mapOptions"
      style="height: 92.5%; width: 98.1%; position: fixed"
    >
      <l-tile-layer
        :url="url"
        :attribution="attribution"
      />
      <map_marker v-for="marker in markers" :marker="marker" :key="marker.properties.name"></map_marker>

    </l-map>

    <v-navigation-drawer app apppermanent expand-on-hover mini-variant-width="5" width="400" right>
    </v-navigation-drawer>

  </div>
</template>

<script>
import { latLng} from 'leaflet';
import {
  LMap,
  LTileLayer,
  LMarker,
  LPopup,
  LTooltip,
  LFeatureGroup,
  LIcon,
} from 'vue2-leaflet';

import map_marker from "../components/map_components/map_marker"

export default {
  name: "MapPage",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
    LTooltip,
    LFeatureGroup,
    LIcon,
    map_marker,
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
      markers: [
        {
          "type": "Feature",
          "geometry": {
            "type": "Point",
            "coordinates": [53.514797, 28.619385]
          },
          "properties": {
            "name": "Dinagat Islands"
          }
        },
        {
          "type": "Feature",
          "geometry": {
            "type": "Point",
            "coordinates": [53.5, 28.65]
          },
          "properties": {
            "name": "Islands"
          }
        }
      ],
      icon: {
        iconUrl: "icon/test.png",
        iconSize: [48, 48],
        iconAnchor: [16, 37]
      },

      selection: [],
      items: [
        {
          id: 1,
          name: 'Applications :',
          action: 'mdi-ticket',
          children: [
            { id: 2, name: 'Calendar : app' },
            { id: 3, name: 'Chrome : app' },
            { id: 4, name: 'Webstorm : app' },
          ],
        },
        {
          id: 5,
          name: 'Documents :',
          children: [
            {
              id: 6,
              name: 'vuetify :',
              children: [
                {
                  id: 7,
                  name: 'src :',
                  children: [
                    { id: 8, name: 'index : ts' },
                    { id: 9, name: 'bootstrap : ts' },
                  ],
                },
              ],
            },
            {
              id: 10,
              name: 'material2 :',
              children: [
                {
                  id: 11,
                  name: 'src :',
                  children: [
                    { id: 12, name: 'v-btn : ts' },
                    { id: 13, name: 'v-card : ts' },
                    { id: 14, name: 'v-window : ts' },
                  ],
                },
              ],
            },
          ],
        },
        {
          id: 15,
          name: 'Downloads :',
          children: [
            { id: 16, name: 'October : pdf' },
            { id: 17, name: 'November : pdf' },
            { id: 18, name: 'Tutorial : html' },
          ],
        },
        {
          id: 19,
          name: 'Videos :',
          children: [
            {
              id: 20,
              name: 'Tutorials :',
              children: [
                { id: 21, name: 'Basic layouts : mp4' },
                { id: 22, name: 'Advanced techniques : mp4' },
                { id: 23, name: 'All about app : dir' },
              ],
            },
            { id: 24, name: 'Intro : mov' },
            { id: 25, name: 'Conference introduction : avi' },
          ],
        },
      ],
    };
  },
  methods: {
  },
};
</script>

<style>
.sticky {
   position: sticky;
   top: 0;
   z-index: 2;
}
</style>
