<template>
    <v-card>
    <v-card-title class="text-h5 grey lighten-2">
        RADIO TX2 ALARM
    </v-card-title>
    <v-card-text>
        11:20 RADIO TX2 SHUT DOWN
    </v-card-text>

    <v-divider></v-divider>

    <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
        color="primary"
        text
        @click="close"
        >
        close
        </v-btn>
    </v-card-actions>
    </v-card>
</template>

<script>
  export default {
    name: 'Dialog',
    data: () => ({
    }),
    methods:{
      close:function(){
        this.$emit('close');
      }
    },
    watch:{
    },
  }
</script>
<style>
</style>