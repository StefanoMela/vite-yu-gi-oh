<script>
import {store} from '../data/store.js'
import AppCard from "./AppCard.vue";

export default {
  data() {
    return {
      store,
    };
  },

  components: { AppCard },
};
</script>

<template>
  <div class="container py-5">
    <div class="row row-cols-3">
      <AppCard 
      v-for="(character, id) in store.characters"
      :key="id"
      :character="character"/>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
