<template>
  <v-app>
  <v-card>
      <v-tabs
        v-model="tabs"
        fixed-tabs
        background-color="grey lighten-2"
      >
      <v-tabs-slider></v-tabs-slider>
      <v-tab
        href="#main"
      >
        MAIN
      </v-tab>
      <v-tab
        href="#atis_voice"
      >
        ATIS Voice Converter
      </v-tab>
      <v-tab
        href="#atis_watch"
      >
        Trial ATIS Voice
      </v-tab>
      <v-tab
        href="#rec_play"
      >
        Microphone
      </v-tab>
    </v-tabs>

    <v-tabs-items v-model="tabs">
      <v-tab-item value="main">
        <Main/>
      </v-tab-item>
      <v-tab-item value="atis_voice">
        <v-container>
          <img src="img/atis_voice.png" width="100%">
        </v-container>
      </v-tab-item>
      <v-tab-item value="atis_watch">
        <v-container>
          <img src="img/atis_voice.png" width="100%">
        </v-container>
      </v-tab-item>
      <v-tab-item value="rec_play">
        <Microphone/>
      </v-tab-item>
    </v-tabs-items>
  </v-card>

  </v-app>
</template>

<script>
import Main from './components/Main';
import Microphone from './components/Microphone.vue';

export default {
  name: 'App',

  components: {
    Main,
    Microphone,
  },

  data: () => ({
      tabs: null,
      text: 'aaa',
  }),
};
</script>
