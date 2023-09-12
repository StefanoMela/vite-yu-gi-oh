<script>
import AppCard from "./AppCard.vue";


export default {

    components: { AppCard }
};
</script>

<template>
    <div class="container">
        <div class="row row-cols-lg-4 my-3">
            <AppCard />
            <AppCard />
            <AppCard />
            <AppCard />
        </div>
    </div>
</template>

<style lang="scss" scoped></style>
