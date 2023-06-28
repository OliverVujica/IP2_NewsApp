<template>
  <v-app id="inspire">

    <v-toolbar id="navigacija">
      <img class="mr-3" :src="require('../slike/logo5.png')" height="30"/>
      <img class="mr-3" :src="require('../slike/logo2.png')" height="30"/>
     
      <v-title id="title">VUETimes</v-title>

        <v-tabs
        class="elevation-0"
        color="black"
      >
        <v-tab
          v-for="link in links"
          :key="link"
          :to="link.ruta"
        >
          {{ link.ime }}
        </v-tab>
      </v-tabs>
    </v-toolbar>
  
    <v-main>
      <router-view/>
    </v-main>

    <v-bottom-navigation style="background-color: rgb(244, 244, 244);">
        <v-btn @click="toFacebook()">
          <v-icon >mdi-facebook</v-icon>
        </v-btn>

        <v-btn @click="toInstagram()">
          <v-icon>mdi-instagram</v-icon>
        </v-btn>

        <v-btn @click="toTwitter()">
          <v-icon>mdi-twitter</v-icon>
        </v-btn>
     </v-bottom-navigation>

      <v-btn
        fab
        dark
        fixed
        bottom
        right
        color="black"
        @click="returnToTop"
      >
        <v-icon>mdi-arrow-up</v-icon>
      </v-btn>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    links: [
      { ime: 'top stories', ruta: '/' },
      { ime: 'Section', ruta: '/section'},
      { ime: 'Article Search', ruta: '/search' },
      { ime: 'About', ruta: '/about' },
    ],
  }),
  methods: {
      toFacebook: function(){
        window.open('https://www.facebook.com/nytimes/')
      },
       toInstagram: function(){
        window.open('https://www.instagram.com/nytimes/')
      },
       toTwitter: function(){
        window.open('https://twitter.com/nytimes')
      },
      returnToTop: function(){
        window.scrollTo(0, 0);
      }
    },
};
</script>

<style>
#navigacija {
  margin-bottom: 30px;
}
#title {
  padding-right: 10px;
}
</style>