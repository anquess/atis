<template>
  <v-container fluid>
  <v-row class="ma-2">
    <v-col cols="3" class="pa-2">
      <v-row>
        <v-select
          v-model="item"
          :items="items"
          v-bind:background-color="color"
          v-bind:color="color"
        ></v-select>
      </v-row>
      <v-row>
        <v-col cols="4">
          BroadCast Status:
        </v-col>
        <v-col cols="8">
        <v-select
          v-model="bs_status"
          :items="bs_statuses"
          v-bind:background-color="bs_color"
          v-bind:color="bs_color"
        ></v-select>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          Radio Source:
        </v-col>
        <v-col cols="8">
          {{src}}
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          REC TIME:
        </v-col>
        <v-col cols="8">
          {{recTime}}
        </v-col>
      </v-row>
    </v-col>
    <v-col cols="5" class="pa-2">
      <v-row>
        <v-col cols="12">
        <v-card>
          <v-card-title>
            Source ATIS Infomation
          </v-card-title>
          <v-card-text>
            <div class="u-pre-wrap" v-text="atis"></div>
          </v-card-text>
        </v-card>
        </v-col>
      </v-row>
    </v-col>
    <v-col cols="4" class="pa-2">
      <v-row>
        <v-col cols="12">
          <v-card>
            <v-card-title>
              RADIO
            </v-card-title>
            <v-card-text>
              <v-row>
                <v-col cols="4"><v-card-title>TX</v-card-title></v-col>
                <v-col cols="4">
                  <v-row>{{tx1.status}}</v-row>
                  <v-row><v-btn v-bind:color="tx1.color" @click="tx">TX1</v-btn></v-row>
                </v-col>
                <v-col cols="4">
                  <v-row>{{tx2.status}}</v-row>
                  <v-row><v-btn v-bind:color="tx2.color" @click="tx">TX2</v-btn></v-row>
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="4"><v-card-title>RX</v-card-title></v-col>
                <v-col cols="4">
                  <v-row>{{rx1.status}}</v-row>
                  <v-row><v-btn v-bind:color="rx1.color" @click="rx">RX1</v-btn></v-row>
                </v-col>
                <v-col cols="4">
                  <v-row>{{rx2.status}}</v-row>
                  <v-row><v-btn v-bind:color="rx2.color" @click="rx">RX2</v-btn></v-row>
                </v-col>
              </v-row>
            </v-card-text>
          </v-card>
          <v-card>
            <v-card-title>
              CCS ATIS
            </v-card-title>
            <v-card-text>
              <v-row>
                <v-col cols="4"><v-card-title>Converter</v-card-title></v-col>
                <v-col cols="4">
                  <v-row>{{no1.status}}</v-row>
                  <v-row><v-btn v-bind:color="no1.color" @click="atischange">No.1</v-btn></v-row>
                </v-col>
                <v-col cols="4">
                  <v-row>{{no2.status}}</v-row>
                  <v-row><v-btn v-bind:color="no2.color" @click="atischange">No.2</v-btn></v-row>
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="4"><v-card-title>BroadCast Desk</v-card-title></v-col>
                <v-col cols="4">
                  <v-row>{{no1.status}}</v-row>
                  <v-row><v-btn v-bind:color="no1.color" @click="atischange">No.1</v-btn></v-row>
                </v-col>
                <v-col cols="4">
                  <v-row>{{no2.status}}</v-row>
                  <v-row><v-btn v-bind:color="no2.color" @click="atischange">No.2</v-btn></v-row>
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
  export default {
    name: 'Main',
    data: () => ({
      tx1: { color: "green", status: "act" },
      tx2: { color: "green", status: "stb" },
      rx1: { color: "green", status: "act" },
      rx2: { color: "green", status: "stb" },
      no1: { color: "green", status: "act" },
      no2: { color: "grey", status: "stb" },
      color: 'green',
      item:"Auto",
      items: ["Auto","SemiAuto","Manual"],
      bs_color: 'green',
      bs_status:"ON AIR",
      bs_statuses: ["ON AIR","OFF AIR","DIRECT","PROGRUM CUT"],
      src:"音声自動化装置",
      recTime:"1:30",
      atis:"ATIS RJTT G\nM1100\n(APCH)ILS RWY32L APCH\n",
    }),
    watch:{
      item: function(val) {
        if (val === "Auto") {
          this.color = "green"
        }else if(val === "SemiAuto"){
          this.color = "blue"
        }else{
          this.color = "orange"
        }
      },
      bs_status: function(val) {
        if (val === "ON AIR") {
          this.bs_color = "green"
        }else if(val === "DIRECT"){
          this.bs_color = "orange"
        }else{
          this.bs_color = "gray"
        }
      },
    },
    methods:{
      tx: function() {
        if(this.tx1.status==="act"){
          this.tx1 = { color: "grey", status: "stb" };
          this.tx2 = { color: "green", status: "act" };
        }else{
          this.tx1 = { color: "green", status: "act" };
          this.tx2 = { color: "green", status: "stb" };
        }
      },
      rx: function() {
        if(this.rx1.status==="act"){
          this.rx1 = { color: "red", status: "stb" };
          this.rx2 = { color: "green", status: "act" };
        }else{
          this.rx1 = { color: "green", status: "act" };
          this.rx2 = { color: "green", status: "stb" };
        }
      },
      atischange: function() {
        if(this.no1.status==="act"){
          this.no1 = { color: "grey", status: "stb" };
          this.no2 = { color: "green", status: "act" };
        }else{
          this.no1 = { color: "green", status: "act" };
          this.no2 = { color: "grey", status: "stb" };
        }
      },
    },
  }
</script>
<style>
.green{
    background-color: green;
}
.blue{
    background-color: blue;
}
.orange{
    background-color: orange;
}
.gray{
  background-color: gray;
}
.u-pre-wrap {
  white-space: pre-wrap;
}
</style>