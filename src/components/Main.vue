<template>
    <main>
        <!-- UPCOMING -->
        <ListSection v-show="movies.length === 0 && tv.length === 0" :title="'Upcoming Movies'" :list="upcome" @getDetails="showDetails"/>
        <!-- POPULAR MOVIE -->
        <ListSection v-show="movies.length === 0 && tv.length === 0" :title="'Popular Movies'" :list="popMovies" @getDetails="showDetails"/>

        <!-- POPULAR TV -->
        <ListSection v-show="movies.length === 0 && tv.length === 0" :title="'Popular TV Shows'" :list="popTV" @getDetails="showDetails"/>

        <!-- MOVIES LIST -->
        <ListSection v-show="movies.length != 0" :title="'Movies'" :list="movies" @getDetails="showDetails"/>

        <!-- TV LIST -->
        <ListSection v-show="tv.length != 0" :title="'TV Shows'" :list="tv" @getDetails="showDetails"/>

        <!-- DETAILS -->
        <Details v-if="detailsVisibility" :details="details" @close="closeDetails"/>
    </main>
</template>

<script>
// COMPONENTS
import ListSection from '@/components/ListSection.vue';
import Details from '@/components/Details.vue';

export default {
    name: 'Main',
    components: {
        ListSection,
        Details,
    },
    props: {
        movies: Array,
        tv: Array,
        popMovies: Array,
        popTV: Array,
        upcome: Array,
    },
    data(){
        return {
            details: {},
            detailsVisibility: false,
        }
    },
    methods: {
        showDetails(obj){
            this.details = obj;
            this.detailsVisibility = true;
        },
        closeDetails(){
            this.detailsVisibility = false;
        },
    }
}
</script>

<style scoped lang="scss">
// SCSS VARIABLES
@import '../Styles/variables.scss';

    main{
        padding: 0 20px;
    }
</style>