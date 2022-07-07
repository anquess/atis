<template>
  <v-dialog v-model="show" :max-width="400">
    <v-card>
      <div v-if="title==='Info'">
      <v-card-title class="primary white--text" primary-title>
        {{ title }}
      </v-card-title>
      </div>
      <div v-else>
      <v-card-title class="error white--text" primary-title>
        {{ title }}
      </v-card-title>
      </div>
      <v-card-text class="pa-4">
        <p>{{ message }}</p>
      </v-card-text>
      <v-divider></v-divider>
      <v-card-actions>
        <v-spacer></v-spacer>
        <div v-if="is_confirm">
        <v-btn @click="ok">
          OK
        </v-btn>
        <v-btn @click="close">
          Cancel
        </v-btn>
        </div>
        <div v-else>
        <v-btn @click="close">
          閉じる
        </v-btn>
        </div>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<style lang="scss" scoped></style>

<script>
export default {
  name: 'Confirm',
  props:["title", "is_confirm", "message", "show"],
  methods:{
      close:function(){
        this.$emit('close');
      },
      ok:function(){
        this.$emit('ok');
      },
  }
}
</script>