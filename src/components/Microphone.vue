<template>
  <v-container fluid>
    <v-row>
      <v-col cols="4">
        <v-card>
          <v-row class="d-flex justify-center mb-6">
            <p>ダイレクト録音</p>
          </v-row>
          <v-row class="d-flex justify-center mb-6">
            <v-col cols="12">
              <div class="text-center">
                <v-btn
                  id="direct"
                  class="mx-2"
                  @click="directrec = !directrec"
                  fab
                  dark
                  small
                  color="primary"
                >
                  <div v-if="directrec"><v-icon dark>mdi-stop</v-icon></div>
                  <div v-else><v-icon dark>mdi-microphone</v-icon></div>
                </v-btn>
                <v-btn
                  class="mx-2"
                  v-if="directrec"
                  @click="directrec = !directrec"
                  fab
                  dark
                  small
                  color="primary"
                >
                  <div><v-icon dark>mdi-pause</v-icon></div>
                </v-btn>
                <v-slider
                  hint="rec and play bar"
                  max="1500"
                  min="0"
                  v-model="directrecPos"
                ></v-slider>
              </div>
            </v-col>
          </v-row>
        </v-card>
        <v-card>
          <v-row class="d-flex justify-center mb-6">
            <p>マニュアル録音</p>
          </v-row>
          <v-row class="d-flex justify-center mb-6">
            <v-col cols="12">
              <div class="text-center">
                <v-btn
                  class="mx-2"
                  @click="rec = !rec"
                  fab
                  dark
                  small
                  color="primary"
                >
                  <div v-if="rec"><v-icon dark>mdi-stop</v-icon></div>
                  <div v-else><v-icon dark>mdi-microphone</v-icon></div>
                </v-btn>
                <v-slider
                  hint="rec and play bar"
                  max="1500"
                  min="0"
                  v-model="recPos"
                ></v-slider>
              </div>
            </v-col>
          </v-row>
        </v-card>
        <v-card>
          <v-row class="d-flex justify-center mb-6">
            <p>録音音声試聴</p>
          </v-row>
          <v-row class="d-flex justify-center mb-6">
            <v-col cols="12">
              <div class="text-center">
                <v-btn
                  class="mx-2"
                  @click="play = !play"
                  fab
                  dark
                  small
                  color="primary"
                >
                  <div v-if="play"><v-icon dark>mdi-stop</v-icon></div>
                  <div v-else><v-icon dark>mdi-play</v-icon></div>
                </v-btn>
                <v-slider
                  hint="rec and play bar"
                  max="1500"
                  min="0"
                  v-model="playPos"
                ></v-slider>
              </div>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
      <v-col cols="8">
        <v-card>
          <v-card-title> ATIS情報 </v-card-title>
          <v-card-text>
            <atisinfo :atis="atis" />
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Atisinfo from "./AtisInfo.vue";
export default {
  name: "Microphone",
  components: {
    Atisinfo,
  },

  props: ["atis"],
  data: () => ({
    directrec: false,
    directrecPos: 0,
    rec: false,
    recPos: 0,
    play: false,
    playPos: 0,
  }),
  methods: {
    updateTime: function () {
      if (this.directrec) {
        this.directrecPos = this.directrecPos + 1;
      }
      if (this.rec) {
        this.recPos = this.recPos + 1;
      }
      if (this.play) {
        this.playPos = this.playPos + 1;
      }
    },
  },
  watch: {},
  mounted: function () {
    setInterval(this.updateTime, 100);
  },
};
</script>
<style>
</style>