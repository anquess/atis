<template>
  <v-container>
    <v-data-table
      :headers="headers"
      :items="atis"
      class="resizable-column"
      hide-default-footer
    />
  </v-container>
</template>
<script>
export default {
  name: "Atisinfo",
  props: ["atis"],
  data() {
    return {
      headers: [
        { text: "No", value: "no", align: "left", sortable: false },
        {
          text: "Description",
          value: "description",
          align: "left",
          sortable: false,
        },
      ],
    };
  },
};
</script>
<style>
</style>

