<template>
  <v-app>
    <v-card>
      <v-toolbar color="grey lighten-2">
        <v-row>
          <v-col cols="10">
            <v-toolbar-title>RJCH 函館空港ATIS</v-toolbar-title>
          </v-col>
          <v-col cols="2">
            <nested-menu icon='mdi-dots-vertical' color="grey lighten-2" :menu-items='fileMenuItems' @nested-menu-click='onMenuItemClick' />
          </v-col>
        </v-row> 
      </v-toolbar>
    </v-card>
    <v-card>
      <v-tabs v-model="tabs" fixed-tabs background-color="grey lighten-2">
        <v-tabs-slider></v-tabs-slider>
        <v-tab href="#AUTO"> MAIN </v-tab>
        <v-tab href="#atis_voice"> 音声自動 </v-tab>
        <v-tab href="#atis_watch"> 音声自動試聴 </v-tab>
        <v-tab href="#rec_play"> 放送卓 </v-tab>
        <v-tab href="#rec">録音 </v-tab>
      </v-tabs>

      <v-tabs-items v-model="tabs">
        <v-tab-item value="AUTO">
          <Main :atis="atis" @direct="direct" />
        </v-tab-item>
        <v-tab-item value="atis_voice">
          <v-container>
            <img src="img/atis_voice.png" width="100%" />
          </v-container>
        </v-tab-item>
        <v-tab-item value="atis_watch">
          <v-container>
            <img src="img/atis_trial.png" width="100%" />
          </v-container>
        </v-tab-item>
        <v-tab-item value="rec_play">
          <Microphone :atis="atis" />
        </v-tab-item>
        <v-tab-item value="rec">
          <v-container>
            <img src="img/rec.png" width="100%" />
          </v-container>
        </v-tab-item>
    </v-tabs-items>
    </v-card>
    <div class="text-center">
      <Confirm :show="confirm" :is_confirm="is_confirm" :is_move_atis_voice="is_move_atis_voice" :title="confirm_title" :message="confirm_message" @close="close" @close2="change_direct_atis_voice" @ok="change_direct" />
      <v-btn color="red lighten-2" dark @click="delay_open"> Test Alart </v-btn>
      少し遅れてアラートのダイアログが表示されます。
    </div>
  </v-app>
</template>

<script>
import Main from "./components/Main";
import Microphone from "./components/Microphone.vue";
import Confirm from "./components/Confirm.vue";
import NestedMenu from "./components/NestedMenu.vue";

export default {
  name: "App",

  components: {
    Main,
    Microphone,
    Confirm,
    NestedMenu,
  },

  data: () => ({
    fileMenuItems: [
      {
        name: '辞書',
        menu: [
          { name: '単語辞書登録', window: 'jisho_tango.png' },
          { name: '音声辞書登録', window: 'jisho_onseijisho.png' },
          { name: '単語分解辞書登録', window: 'jisho_tangobunkai.png' },
          { name: '文節変換辞書登録', window: 'jisho_bunsetsujisho.png' },
          { name: 'センテンス形式辞書登録', window: 'jisho_sentens.png' },
          { name: 'カテゴリ登録', window: 'jisho_category.png' },
          { name: '辞書更新履歴', window: 'jisho_rireki.png' },
          { name: '辞書同期', },
          { name: '辞書バックアップ', window: 'jisho_backup.png' },
          { name: '辞書リストア', window: 'jisho_restore.png' },
        ]
      },
      {
        name: 'ユーティリティ',
        menu: [
          { name: '記録データ', window: 'utl_kirokudata.png' },
          { name: 'ログデータ取り出し', window: 'utl_backup.png' },
          { name: 'セットアップ' },
        ]
      },
    ],
    tabs: null,
    text: "aaa",
    dialog: false,
    confirm:false,
    confirm_title : "test_title",
    confirm_message : "test_message",
    is_confirm: false,
    is_move_atis_voice: false,
    alert_message_index: 0,
    alert_messages:[
      {
        title: "Alert",
        message : "Tx1 障害",
        },
      {
        title: "Info",
        message : "ATIS情報を受信しました。",
        },
      {
        title: "Alert",
        message : "ATIS情報の変換に失敗しました"
      },
    ],
    atis: [
      {
        no: 3,
        description: "MS0530",
      },
      {
        no: 4,
        description: "(APCH)ILS Y RWY01R",
      },
      {
        no: 5,
        description: "LDG RWY 01R",
      },
      {
        no: 6,
        description: "DEP RWY 01L",
      },
      {
        no: 7,
        description: "DEP FREQ 124.7",
      },
      {
        no: 8,
        description: "MOD ICE AND GR OBS AT 0440Z YUNEY",
      },
      {
        no: 8,
        description: "TO PUNCH BTN 4000FT AND 3000FT IN",
      },
      {
        no: 8,
        description: "DES B772",
      },
      {
        no: 9,
        description: "MS",
      },
      {
        no: 9,
        description: "270530 35007KT 20KM R01L//// M////",
      },
      {
        no: 9,
        description: "E//// R01R/1800U -TSRA BR",
      },
      {
        no: 9,
        description: "FEW005ST BKN020CB 16/15 Q10009/A2979",
      },
      {
        no: 9,
        description: "RMK 4000NE-SE FBL TS 10KM NE-SE",
      },
      {
        no: 9,
        description: "MOV SE=",
      },
      {
        no: 10,
        description: "Q/TWO NINE SEVEN NINE",
      },
      {
        no: 11,
        description: "ADVISE YOU HAVE INFORMATION Y",
      },
    ],
  }),
  methods: {
    delay_open: function () {
      if(this.alert_message_index === 2){
        this.is_move_atis_voice = true;
      }else{
        this.is_move_atis_voice = false;
      }
      this.is_confirm = false;
      this.confirm_title = this.alert_messages[this.alert_message_index].title;
      this.confirm_message = this.alert_messages[this.alert_message_index].message;
      this.alert_message_index = (this.alert_message_index + 1) % 3;
      window.setTimeout(this.open, 1000);
    },
    open: function() {
      this.confirm = true;
    },
    close: function() {
      this.confirm = false;
    },
    direct: function () {
      this.is_confirm = true;
      this.is_move_atis_voice = false;
      this.confirm_title = "確認";
      this.confirm_message = "放送を中止しダイレクト録音を開始していいいですか？";
      this.open();
    },
    change_direct: function () {
      this.close();
      this.tabs = "rec_play";
    },
    change_direct_atis_voice: function () {
      this.close();
      this.tabs = "atis_voice";
    },
    onMenuItemClick (item) {
      console.log(`onMenuItemClick(), item=${item}`)
      if (item.window) {
        window.open('img/' + item.window, item.name);
      }
    },
  },
};
</script>
