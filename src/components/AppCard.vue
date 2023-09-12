<script>
import { store } from "../data/store.js";

export default {
 props: {character: Object}
};
</script>

<template>
  <div class="card">
    <img :src="character.card_images[0].image_url" class="card-img-top" alt="" />
    <div class="card-body">
      <h5 class="card-title">{{ character.name }}</h5>
      <p class="card-text">{{ character.archetype }}</p>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
