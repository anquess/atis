<template>
  <v-container fluid>
    <v-row class="ma-2">
      <v-col cols="3" class="pa-2">
        <v-row>
          <v-col cols="6"> 音声自動化操作モード： </v-col>
          <v-col cols="6">
            <v-select
              v-model="item"
              :items="items"
              v-bind:background-color="color"
              v-bind:color="color"
            ></v-select>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="6"> 放送卓: </v-col>
          <v-col cols="6">
            <v-select
              v-model="bs_status"
              :items="bs_statuses"
              v-bind:background-color="bs_color"
              v-bind:color="bs_color"
            ></v-select>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="6"> 放送音源: </v-col>
          <v-col cols="6">
            {{ src }}
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="6"> 放送音源時間: </v-col>
          <v-col cols="6">
            {{ recTime }}
          </v-col>
        </v-row>
      </v-col>
      <v-col cols="5" class="pa-2">
        <v-row>
          <v-col cols="12">
            <v-card>
              <v-card-title> ATIS情報 </v-card-title>
              <v-card-text>
                <atisinfo :atis="atis" />
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
      <v-col cols="4" class="pa-2">
        <v-row>
          <v-col cols="12">
            <v-card>
              <v-card-title> 送受信機状態 </v-card-title>
              <v-card-text>
                <v-row>
                  <v-col cols="6"><v-card-title>送信機</v-card-title></v-col>
                  <v-col cols="3">
                    <v-row>{{ tx1.status }}</v-row>
                    <v-row
                      ><v-btn v-bind:color="tx1.color" @click="tx"
                        >TX1</v-btn
                      ></v-row
                    >
                  </v-col>
                  <v-col cols="3">
                    <v-row>{{ tx2.status }}</v-row>
                    <v-row
                      ><v-btn v-bind:color="tx2.color" @click="tx"
                        >TX2</v-btn
                      ></v-row
                    >
                  </v-col>
                </v-row>
                <v-row>
                  <v-col cols="6"><v-card-title>受信機</v-card-title></v-col>
                  <v-col cols="3">
                    <v-row>{{ rx1.status }}</v-row>
                    <v-row
                      ><v-btn v-bind:color="rx1.color" @click="rx"
                        >RX1</v-btn
                      ></v-row
                    >
                  </v-col>
                  <v-col cols="3">
                    <v-row>{{ rx2.status }}</v-row>
                    <v-row
                      ><v-btn v-bind:color="rx2.color" @click="rx"
                        >RX2</v-btn
                      ></v-row
                    >
                  </v-col>
                </v-row>
              </v-card-text>
            </v-card>
            <v-card>
              <v-card-title> 放送卓状態 </v-card-title>
              <v-card-text>
                <v-row>
                  <v-col cols="6"
                    ><v-card-title>音声自動化機能</v-card-title></v-col
                  >
                  <v-col cols="3">
                    <v-row>{{ no1.status }}</v-row>
                    <v-row
                      ><v-btn v-bind:color="no1.color" @click="atischange"
                        >No.1</v-btn
                      ></v-row
                    >
                  </v-col>
                  <v-col cols="3">
                    <v-row>{{ no2.status }}</v-row>
                    <v-row
                      ><v-btn v-bind:color="no2.color" @click="atischange"
                        >No.2</v-btn
                      ></v-row
                    >
                  </v-col>
                </v-row>
                <v-row>
                  <v-col cols="6"><v-card-title>放送卓</v-card-title></v-col>
                  <v-col cols="3">
                    <v-row>{{ no1.status }}</v-row>
                    <v-row
                      ><v-btn v-bind:color="no1.color" @click="atischange"
                        >No.1</v-btn
                      ></v-row
                    >
                  </v-col>
                  <v-col cols="3">
                    <v-row>{{ no2.status }}</v-row>
                    <v-row
                      ><v-btn v-bind:color="no2.color" @click="atischange"
                        >No.2</v-btn
                      ></v-row
                    >
                  </v-col>
                </v-row>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Atisinfo from "./AtisInfo.vue";
export default {
  name: "Main",
  components: {
    Atisinfo,
  },

  props: ["atis"],
  data: () => ({
    tx1: { color: "green", status: "act" },
    tx2: { color: "green", status: "stb" },
    rx1: { color: "green", status: "act" },
    rx2: { color: "green", status: "stb" },
    no1: { color: "green", status: "act" },
    no2: { color: "grey", status: "stb" },
    color: "green",
    item: "音声自動変換",
    items: ["音声自動変換", "音声半自動変換", "手動変換"],
    bs_color: "green",
    bs_status: "音声自動録音放送",
    bs_statuses: [
      "音声自動録音放送",
      "放送中止",
      "プログラムカット",
      "ダイレクト録音放送",
    ],
    src: "音声自動化装置",
    recTime: "1:30",
  }),
  watch: {
    item: function (val) {
      if (val === "音声自動変換") {
        this.color = "green";
      } else if (val === "音声半自動変換") {
        this.color = "blue";
      } else {
        this.color = "orange";
      }
    },
    bs_status: function (val) {
      if (val === "音声自動録音放送") {
        this.bs_color = "green";
      } else if (val === "ダイレクト録音放送") {
        this.bs_color = "orange";
        this.$emit("direct");
      } else {
        this.bs_color = "gray";
      }
    },
  },
  methods: {
    tx: function () {
      if (this.tx1.status === "act") {
        this.tx1 = { color: "grey", status: "stb" };
        this.tx2 = { color: "green", status: "act" };
      } else {
        this.tx1 = { color: "green", status: "act" };
        this.tx2 = { color: "green", status: "stb" };
      }
    },
    rx: function () {
      if (this.rx1.status === "act") {
        this.rx1 = { color: "red", status: "stb" };
        this.rx2 = { color: "green", status: "act" };
      } else {
        this.rx1 = { color: "green", status: "act" };
        this.rx2 = { color: "green", status: "stb" };
      }
    },
    atischange: function () {
      if (this.no1.status === "act") {
        this.no1 = { color: "grey", status: "stb" };
        this.no2 = { color: "green", status: "act" };
      } else {
        this.no1 = { color: "green", status: "act" };
        this.no2 = { color: "grey", status: "stb" };
      }
    },
  },
};
</script>
<style>
.green {
  background-color: green;
}
.blue {
  background-color: blue;
}
.orange {
  background-color: orange;
}
.gray {
  background-color: gray;
}
.u-pre-wrap {
  white-space: pre-wrap;
}
</style>