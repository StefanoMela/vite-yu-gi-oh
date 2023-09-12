<script>
import axios from "axios";
import { store } from "./data/store.js";

import AppMain from "./components/AppMain.vue";
import AppCard from "./components/AppCard.vue";

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

        console.log(response);
        const charactersData = response.data.data.map((character) => {
          const { id, name, archetype, card_images } = character;
          return { id, name, archetype, card_images };
        });

        store.characters = charactersData;

        const { next } = response.data.meta.next_page;
        store.pagination = {next};
      });
    },

    nextPage() {
      if (!store.pagination.next) return;
      this.fetchCharacters(store.pagination.next);
    },
  },

  created() {
    this.fetchCharacters(store.apiUrl);
  },
};
</script>

<template>
  <div class="header text-center">
    <h1 class="mt-5">YU-GI-HO Cards</h1>
  </div>
  <nav
    class="d-flex justify-content-center mt-5"
  >
    <ul class="pagination">
      <li class="page-item"><a class="page-link" href="#">Previous</a></li>
      <li class="page-item"><a class="page-link" href="#" @onclick="nextPage()">Next</a></li>
    </ul>
  </nav>
  <AppMain />
</template>

<style lang="scss" scoped></style>
