<template>
    <v-btn-toggle
    v-model="toggle_exclusive"
    mandatory
    >
    <v-btn>
        <v-icon>mdi-format-align-left</v-icon>
    </v-btn>
    <v-btn>
        <v-icon>mdi-format-align-center</v-icon>
    </v-btn>
    <v-btn>
        <v-icon>mdi-format-align-right</v-icon>
    </v-btn>
    <v-btn>
        <v-icon>mdi-format-align-justify</v-icon>
    </v-btn>
    </v-btn-toggle>
</template>

<script>
  export default {
    data () {
      return {
        toggle_exclusive: undefined,
      }
    },
  }
</script>
<!--
<template>
    <div>
        <v-overflow-btn
            :items="dropdown_font"
            label="Select font"
            hide-details
            class="pa-0"
        ></v-overflow-btn>
    </div>
</template>

<script>
export default {
    name: 'Edit-text'
}
</script>
-->