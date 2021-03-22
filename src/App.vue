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
          <v-text-field v-model="login" label="Name" required></v-text-field>

          <v-text-field v-model="password" label="password" required></v-text-field>


          <v-btn
            color="error"
            class="mr-4"
            @click="loginInSystem"
          >
            login
          </v-btn>
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
const axios = require('axios').default;
// axios.defaults.xsrfHeaderName = "X-CSRFToken"
// axios.defaults.xsrfCookieName = 'csrftoken'
// axios.defaults.withCredentials = true

export default {
  name: 'App',
  data: () => ({
      tab: null,
    login: '',
    password: '',
  }),
  methods: {
    loginInSystem(){
      axios.post('http://127.0.0.1:8000/auth/login/', {
        login: this.login,
        password: this.password
      })
      .then(function (response) {
        console.log(response);
      })
    }
  }
};
</script>

<style>

</style>
