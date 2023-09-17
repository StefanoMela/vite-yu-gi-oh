<script>
import { store } from "../data/store";

export default {
  data() {
    return {
      searchedTerm: "",
      archetypeSearch: "",
      store,
    };
  },

  props: {
    placeholder: String,
    buttonText: String,
    buttonResetText: String,
  },

  emits: ["form-submit", "archetype-search"],

  methods: {
    searchReset() {
      this.searchedTerm = "";
      this.$emit("form-submit", this.searchedTerm);
    },
  },
};
</script>

<template>
  <select
    class="form-select form-select-lg mb-3"
    aria-label="Large select example"
    @change="$emit('archetype-search', archetypeSearch)"
    v-model="archetypeSearch"
  >
    <option selected value="all-archetypes">Cerca per archetipo</option>
    <option
      v-for="archetype in store.archetypes"
      :value="archetype.archetype_name"
    >
      {{ archetype.archetype_name }}
    </option>
  </select>

  <form
    @submit.prevent="$emit('form-submit', searchedTerm)"
    class="d-flex w-75"
    role="search"
  >
    <input
      v-model="searchedTerm"
      :placeholder="placeholder || 'Cerca...'"
      class="form-control me-2"
      type="search"
      aria-label="Search"
    />
    <button class="btn btn-primary" type="submit">
      {{ buttonText || "Cerca !" }}
    </button>
    <button @click="searchReset()" class="btn btn-warning" type="submit">
      {{ buttonResetText || "Reset" }}
    </button>
  </form>
</template>

<style lang="scss" scoped></style>
