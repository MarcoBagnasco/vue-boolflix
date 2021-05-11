<template>
  <div id="app">
    <!-- APP HEADER -->
    <Header @search="searchTitle"/>

    <!-- APP MAIN -->
    <Main :movies="moviesList" :tv="tvList" :popMovies="popularMovies" :popTV="popularTV" :upcome="up"/>
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
      moviesList: [],
      tvList: [],
      popularMovies: [],
      popularTV: [],
      up: [],
    }
  },
  created(){
    this.popularTitle();
    this.upcoming();
  },
  methods:{
    upcoming(){
            // Call API Movies
      axios.get('https://api.themoviedb.org/3/movie/upcoming', {
        params: {
          api_key: 'dabed2596a83196385f10dd2ac69a20d',
        }
      })
      .then(res => {
        this.up = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });
    },
    popularTitle(){
      // Call API Movies
      axios.get('https://api.themoviedb.org/3/movie/popular', {
        params: {
          api_key: 'dabed2596a83196385f10dd2ac69a20d',
        }
      })
      .then(res => {
        this.popularMovies = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });

      // Call API TV Shows
      axios.get('https://api.themoviedb.org/3/tv/popular', {
        params: {
          api_key: 'dabed2596a83196385f10dd2ac69a20d',
        }
      })
      .then(res => {
        this.popularTV = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });
    },
    searchTitle(search){
      // Call API Movies
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: 'dabed2596a83196385f10dd2ac69a20d',
          query: search,
        }
      })
      .then(res => {
        this.moviesList = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });

      // Call API TV Shows
      axios.get('https://api.themoviedb.org/3/search/tv', {
        params: {
          api_key: 'dabed2596a83196385f10dd2ac69a20d',
          query: search,
        }
      })
      .then(res => {
        this.tvList = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });
    }
  }
}
</script>

<style lang="scss">
// GENERAL
@import './Styles/general.scss';
</style>
