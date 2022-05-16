<template>
  <v-container>
    <Edit_text/>
    <v-tabs
      v-model="tab"
      grow
    >
      <v-tab
        v-for="item in items"
        :key="item.tab"
      >
        {{ item.tab }}
      </v-tab>
      <!-- <component :is="currentView" :mainId="data.mainId" :keyId="data.keyId" /> -->
    </v-tabs>

    <v-tabs-items v-model="tab">
      <v-tab-item
        v-for="item in items"
        :key="item.tab"
      >
        <v-card flat>
          <v-card-text>{{ item.content }}</v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </v-container>  
</template>

<script>
import Edit_text from './Edit-text.vue';

export default {
  name: 'Menu-right',

  components: {
    Edit_text,
  },

  data: () => ({
    tab: null,
    items: [
      { tab: '디자인', content: 'Tab 1 Content' },
      { tab: '글꼴', content: '글꼴' },
      { tab: '객체 리스트', content: 'Tab 3 Content' },
    ]
  })
};
</script>

<style scoped>
div {
  flex: 1; 
  background-color: #EEEEEE;
}
</style>>