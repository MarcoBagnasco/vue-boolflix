<template>
  <div id="app">
    <!-- APP HEADER -->
    <Header @search="searchTitle" @clear="clearPage" @showMy="showMyList"/>

    <!-- APP MAIN -->
    <Main :search="searchString" :movies="moviesList" :tv="tvList" :popMovies="popularMovies" :popTV="popularTV" :upcome="up" :showMy="viewMy"/>
  </div>
</template>

<script>
// AXIOS
import axios from 'axios';

// COMPONENTS
import Header from '@/components/Header.vue';
import Main from '@/components/Main.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main,
  },
  data(){
    return {
      apiURL: 'https://api.themoviedb.org/3/',
      api_key: 'dabed2596a83196385f10dd2ac69a20d',
      moviesList: [],
      tvList: [],
      searchString: '',
      popularMovies: [],
      popularTV: [],
      up: [],
      viewMy: false,
    }
  },
  created(){
    this.popularTitle();
    this.upcoming();
  },
  methods:{
    /**
     * Show MyList
     */
    showMyList(){
      this.viewMy = true;
    },

    /**
     * Reset page
     */
    clearPage(){
        this.searchString = '',
        this.moviesList = [];
        this.tvList = [];
        this.viewMy = false;
        window.scrollTo(0, 0);
    },

    /**
     * Call API for upcoming movie
     */
    upcoming(){
      const apiParams = {
        api_key: this.api_key,
      }
      
      axios.get(`${this.apiURL}movie/upcoming`, {
        params: apiParams,
      })
      .then(res => {
        this.up = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });
    },

    /**
     * Call API for popular title
     */
    popularTitle(){
      const apiParams = {
        api_key: this.api_key,
      }
      // Call API Popular Movies
      axios.get(`${this.apiURL}movie/popular`, {
        params: apiParams,
      })
      .then(res => {
        this.popularMovies = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });

      // Call API Popular TV Shows
      axios.get(`${this.apiURL}tv/popular`, {
        params: apiParams,
      })
      .then(res => {
        this.popularTV = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });
    },

    /**
     * Call API based on search and set searchString
     */
    searchTitle(search){
      const apiParams = {
        api_key: this.api_key,
        query: search,
      }
      // Call API Movies
      axios.get(`${this.apiURL}search/movie`, {
        params: apiParams,
      })
      .then(res => {
        this.moviesList = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });

      // Call API TV Shows
      axios.get(`${this.apiURL}search/tv`, {
        params: apiParams,
      })
      .then(res => {
        this.tvList = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });

      this.viewMy = false;
      this.searchString = search;
    }
  }
}
</script>

<style lang="scss">
// GENERAL
@import './Styles/general.scss';
</style>