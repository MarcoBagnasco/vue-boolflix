<template>
    <main>
        <!-- NO RESULTS -->
        <div class="no-results" v-if="(!movies.length && !tv.length) && !showMy && search.length">No results match your search</div>

        <!-- UPCOMING -->
        <ScrollList v-show="(!movies.length && !tv.length) && !showMy && !search.length" :title="'Upcoming Movies'" :list="upcome" @getDetails="showDetails"/>

        <!-- POPULAR MOVIE -->
        <SmallList v-show="(!movies.length && !tv.length) && !showMy && !search.length" :title="'Popular Movies'" :list="popMovies" @getDetails="showDetails"/>

        <!-- POPULAR TV -->
        <SmallList v-show="(!movies.length && !tv.length) && !showMy && !search.length" :title="'Popular TV Shows'" :list="popTV" @getDetails="showDetails"/>

        <!-- SEARCH RESULTS -->
        <!-- Movies List -->
        <ListSection v-show="(movies.length) && !showMy && search.length" :title="'Movies'" :list="movies" :search="search" @getDetails="showDetails"/>
        <!-- TV List -->
        <ListSection v-show="(tv.length) && !showMy && search.length" :title="'TV Shows'" :list="tv" :search="search" @getDetails="showDetails"/>

        <!-- MY LIST -->
        <ListSection v-show="showMy" :title="'My List'" :list="myList" @getDetails="showDetails"/>
        <div class="no-title" v-show="myList.length === 0 && showMy">No title in the list</div>

        <!-- DETAILS -->
        <Details v-if="detailsVisibility" :details="details" @close="closeDetails"  :my="myList" @toAdding="addToList" @toRemove="removeFromList"/>
    </main>
</template>

<script>
// COMPONENTS
import ListSection from '@/components/ListSection.vue';
import Details from '@/components/Details.vue';
import SmallList from '@/components/SmallList.vue';
import ScrollList from '@/components/ScrollList.vue';

export default {
    name: 'Main',
    components: {
        ListSection,
        Details,
        SmallList,
        ScrollList,
    },
    props: {
        search: String,
        movies: Array,
        tv: Array,
        popMovies: Array,
        popTV: Array,
        upcome: Array,
        showMy: Boolean,
    },
    data(){
        return {
            details: {},
            detailsVisibility: false,
            myList: [],
        }
    },
    methods: {
        /**
         * Show Details Window
         */
        showDetails(obj){
            this.details = obj;
            this.detailsVisibility = true;
        },

        /**
         * Close Details Window
         */
        closeDetails(){
            this.detailsVisibility = false;
        },
        
        /**
         * Add title to personal list
         */
        addToList(obj){
            if(!this.myList.includes(obj)){
                this.myList.push(obj);
            }
        },

        /**
         * Remove title from personal list
         */
        removeFromList(obj){
            if(this.myList.includes(obj)){
                this.myList.splice(this.myList.indexOf(obj), 1);
            }
        }
    }
}
</script>

<style scoped lang="scss">
// SCSS VARIABLES
@import '../Styles/variables.scss';

    main{
        padding: 0 20px;

        .no-results,
        .no-title{
            font-size: 1.5em;
            text-align: center;
        }
    }
</style>