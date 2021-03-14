<template>
  <v-app>
    <v-app-bar app clipped-right flat height="10" color="green darken-4">
      <template v-slot:extension>
        <v-tabs v-model="tab" align-with-title dark>
          <v-tabs-slider color="red"></v-tabs-slider>
          <v-tab :to="{ name: 'MapPage' }">
            Map
          </v-tab>
          <v-tab :to="{ name: 'About' }">
            About
          </v-tab>
        </v-tabs>
      </template>
    </v-app-bar>

    <v-main app>
      <v-container fluid style="height: 100%">
        <router-view></router-view>
      </v-container>
    </v-main>

  </v-app>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
      tab: null,
  }),
};
</script>

<style>

</style>
