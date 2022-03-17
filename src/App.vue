<template>
  <v-app>
  <v-card>
    <v-toolbar color="grey lighten-2">
      <v-toolbar-title>RJCH 函館空港ATIS</v-toolbar-title>
    </v-toolbar>
  </v-card>
  <v-card>
      <v-tabs
        v-model="tabs"
        fixed-tabs
        background-color="grey lighten-2"
      >
      <v-tabs-slider></v-tabs-slider>
      <v-tab
        href="#AUTO"
      >
        AUTO
      </v-tab>
      <v-tab
        href="#atis_voice"
      >
        Manual Convert Voice
      </v-tab>
      <v-tab
        href="#atis_watch"
      >
        Trial Convert Voice 
      </v-tab>
      <v-tab
        href="#rec_play"
      >
        Manual BroadCast        
      </v-tab>
    </v-tabs>

    <v-tabs-items v-model="tabs">
      <v-tab-item value="AUTO">
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
    <div class="text-center">
    <v-dialog
      v-model="dialog"
      width="500"
    >
      <Dialog @close="close" />
    </v-dialog>
    <v-btn color="red lighten-2" dark @click="open">
      Test Alart
    </v-btn>
      少し遅れてアラートのダイアログが表示されます。
    </div>
  </v-app>
</template>

<script>
import Main from './components/Main';
import Microphone from './components/Microphone.vue';
import Dialog from './components/Dialog.vue';


export default {
  name: 'App',

  components: {
    Main,
    Microphone,
    Dialog,
  },

  data: () => ({
      tabs: null,
      text: 'aaa',
      dialog: false,
  }),
  methods:{
    open:function(){
      window.setTimeout( this.delay_open, 3000);
    },
    close:function(){
      this.dialog=false;
    },
    delay_open:function(){
      this.dialog=true;
    },
  }
};
</script>
