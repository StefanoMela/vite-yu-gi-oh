<script>
import axios from "axios";
import { store } from "./data/store.js";

import AppMain from "./components/AppMain.vue";
import AppCard from "./components/AppCard.vue";
import SearchBar from "./components/SearchBar.vue";

export default {
  data() {
    return {
      store,

      apiUri: "https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0",

      apiArchetypes: "https://db.ygoprodeck.com/api/v7/archetypes.php",

      apiSearch: "https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=",

      pagination: {
        next: null,
      },
    };
  },

  components: { AppMain, AppCard, SearchBar },

  methods: {
    fetchCharacters(endpoint) {
      axios.get(endpoint).then((response) => {
        // console.log(response);
        store.characters = response.data.data.map((character) => {
          const { id, name, archetype, card_images } = character;
          return { id, name, archetype, card_images };
        });

        const { next } = response.data.meta.next_page;
        this.pagination.next = { next };
      });
    },

    fetchArchetypes(archetypeEndopoint) {
      axios.get(archetypeEndopoint).then((response) => {
        console.log(response.data);
        store.archetypes = response.data;
        console.log(store.archetypes);
      });
    },

    nextPage() {
      if (!this.pagination.next) return;
      this.fetchCharacters(this.pagination.next);
    },

    handleSearch(archetypeSearch) {
      // il parametro può anche cambiare nome rispetto al nome del componente
      const searchEndpoint = `https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=${archetypeSearch}`;
      this.fetchCharacters(searchEndpoint);
    },
  },

  created() {
    this.fetchCharacters(this.apiUri);
    this.fetchArchetypes(this.apiArchetypes);
  },
};
</script>

<template>
  <div class="header text-center">
    <h1 class="mt-5">YU-GI-HO Cards</h1>
  </div>
  <nav class="d-flex justify-content-center mt-5">
    <ul class="pagination">
      <li class="page-item"><a class="page-link" href="#">Previous</a></li>
      <li class="page-item">
        <a class="page-link" href="#" @onclick="nextPage()">Next</a>
      </li>
    </ul>
  </nav>
  <div class="container d-flex justify-content-center flex-wrap">
    <SearchBar
      @form-submit="handleSearch"
      @archetype-search="handleSearch"
      placeholder="Cerca Carte X Archetipo"
      buttonText="Daje"
    />
  </div>
  <AppMain />
</template>

<style lang="scss" scoped></style>
