<template>
    <main>
        <!-- MOVIES LIST -->
        <section class="movies">
            <h2>Movies</h2>
            <div class="list-box">
                <ul class="movies-list flex ai-center">
                    <li v-for="item in movies" :key="item.id">
                        <Card :info="item"/>
                    </li>
                </ul>
            </div>
        </section>

        <!-- TV LIST -->
        <section class="tv">
            <h2>TV Shows</h2>
            <div class="list-box">
                <ul class="tv-list flex ai-center">
                    <li v-for="item in tv" :key="item.id">
                        <Card :info="item"/>
                    </li>
                </ul>
            </div>
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
// SCSS VARIABLES
@import '../Styles/variables.scss';

    h2{
        font-size: 1.8em;
    }
    main{
        padding: 0 20px;
    }
    section{
        margin: 30px 0;
        padding: 30px;
        background-color: $bg-dark-soft;
    }
    .list-box{
        overflow-x: auto;
    }
    ul{
        margin-top: 25px;
    }
    li{
        width: 342px;
        margin: 0 5px;
    }
</style>