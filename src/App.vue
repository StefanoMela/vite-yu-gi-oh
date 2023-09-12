<script>
import axios from "axios";
import { store } from "./data/store.js";

export default {
  data() {
    return {
      store,
    };
  },

  methods: {
    fetchCharacters(endpoint) {
      axios.get(endpoint).then((response) => {

        store.cards = response.data.data;
        console.log(store.cards);

      });
    },
  },

  created() {
    this.fetchCharacters("https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0");
  },
};
</script>

<template>
  <h1>Prova test</h1>
</template>

<style lang="scss" scoped></style>
