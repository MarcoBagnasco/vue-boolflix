<template>
  <div id="app">
      <!-- APP HEADER -->
      <Header @searchMovie="searchMovie"/>

      <!-- APP MAIN -->
      <Main :movies="results"/>
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
      results: [],
    }
  },
  methods:{
    searchMovie(movie){
      // Call API
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: 'dabed2596a83196385f10dd2ac69a20d',
          query: movie,
        }
      })
      .then(res => {
        this.results = res.data.results;
      })
      .catch(err => {
        console.log(err);
      });
    }
  }
}
</script>

<style lang="scss">

</style>
