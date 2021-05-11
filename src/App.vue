<template>
  <div id="app">
    <!-- APP HEADER -->
    <Header @search="searchTitle"/>

    <!-- APP MAIN -->
    <Main :movies="moviesList" :tv="tvList"/>
  </div>
</template>

<script>
import axios from 'axios';

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
    }
  },
  methods:{
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
@import './Styles/General.scss';

</style>
