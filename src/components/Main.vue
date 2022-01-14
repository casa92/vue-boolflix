<template>
    <main class="items-list">
        <ItemCard v-for="movie in movieItemList" :key="movie.id" :description="movie" />
        <ItemCard v-for="series in seriesItemList" :key="series.id" :description="series" />
        
    </main>
</template>

<script>
import ItemCard from './ItemCard.vue';

export default {
    name: "Main",
    components: {
        ItemCard,
    },
    props: {
        movieItemList: [],
        seriesItemList: [],
    }
}
</script>

<style lang="scss" scoped>
    .items-list {
        display: flex;
        overflow-x: auto;
    }
</style>
