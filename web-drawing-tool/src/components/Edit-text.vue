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