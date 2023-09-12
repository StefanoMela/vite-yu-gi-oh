<script>
import { store } from "../data/store.js";
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
    <main>
        <div class="card__container">
          <AppCard
            v-for="(character, id) in store.characters"
            :key="id"
            :character="character"
          />
        </div>
    </main>
</template>

<style lang="scss" scoped>

.card__container {

    display: flex;
    flex-wrap: wrap;
    padding: 1rem;
}

</style>
