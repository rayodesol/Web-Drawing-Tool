<template>
  <v-container>
    <v-text-field
        v-model = "search"
        outlined
        label = "검색"
        background-color = "#FFFFFF"
        type = "text"
        append-icon = "mdi-magnify"
      ></v-text-field>
  </v-container>
</template>

<script>

export default {

  data: () => ({
  
  }),
  methods: {}

};
</script>

<style scoped>
div {
  min-width: 300px;
  max-width: 600px;
  flex: 1;

}

</style>