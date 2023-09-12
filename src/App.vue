<script>
import axios from 'axios';
import { store } from './data/store.js';

import AppMain from './components/AppMain.vue'
import AppCard from './components/AppCard.vue'


export default {
  data() {
    return {
      store,
      
    };
  },

  components: { AppMain, AppCard },

  methods: {
    fetchCharacters(endpoint) {
      axios.get(endpoint).then((response) => {
        

        store.characters = response.data.data;
        console.log(store.characters);
      });
    },

    nextPage(){

      if(!store.next) return;
    }
  },

  created() {
    this.fetchCharacters(store.apiUri);
  },
};
</script>

<template>
<AppMain />
</template>

<style lang="scss" scoped></style>
