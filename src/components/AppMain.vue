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
        <button type="button" class="btn btn-outline-secondary">Previous Page</button>
        <button type="button" class="btn btn-outline-secondary">Next Page</button>
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

main {

    text-align: center;
        button {
            margin-top: 2rem;
            margin-inline: 1rem;
        }

}

.card__container {

    display: flex;
    flex-direction: row;
    justify-content: center;
    flex-wrap: wrap;
    margin: 1.5rem 0;
    padding: 1.5rem;
}

</style>
