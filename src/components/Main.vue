<template>
    <main>
        <!-- MOVIES LIST -->
        <section class="movies">
            <h2>Movies</h2>
            <ol class="movies-list">
                <li v-for="(item, index) in movies" :key="index">
                    <Card :info="item"/>
                </li>
            </ol>
        </section>

        <!-- TV LIST -->
        <section class="movies">
            <h2>TV Shows</h2>
            <ol class="tv-list">
                <li v-for="(item, index) in tv" :key="index">
                    <Card :info="item"/>
                </li>
            </ol>
        </section>

    </main>
</template>

<script>
import Card from '@/components/Card.vue';

export default {
    name: 'Main',
    components: {
        Card,
    },
    props: {
        movies: Array,
        tv: Array,
    },
}
</script>

<style scoped lang="scss">

</style>