<script>
export default {
 props: {character: Object}
};
</script>

<template>
  <div class="card">
    <img :src="character.card_images[0].image_url" class="card-img-top" alt="" />
    <div class="card-body text-center">
      <h5 class="card-title">{{ character.name }}</h5>
      <p class="card-text">{{ character.archetype }}</p>
    </div>
  </div>
</template>

<style lang="scss" scoped>

.card {

  max-width: calc((100% / 5) - 2rem);
  margin-inline: 1rem;
  margin-top: 3rem;
}

</style>
