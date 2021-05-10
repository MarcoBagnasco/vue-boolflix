<template>
  <main>
      <!-- MOVIES LIST -->
      <ol>
          <li v-for="(item, index) in refreshList" :key="index">
              <!-- Movie Info -->
              <ul>
                  <li><strong>Title: </strong>{{item.title !== undefined ? item.title : item.name}}</li>
                  <li><strong>Original Title: </strong>{{item.original_title !== undefined ? item.original_title : item.original_name}}</li>
                  <li>
                      <strong>Language: </strong>
                      <img v-if="item.original_language === 'en'" src="../assets/img/en.png" alt="en flag">
                      <img v-else-if="item.original_language === 'it'" src="../assets/img/it.png" alt="en flag">
                      <span v-else>{{item.original_language}}</span>
                      </li>
                  <li><strong>Vote Average: </strong>{{item.vote_average}}</li>
                  <img src="" alt="">
              </ul>
          </li>
      </ol>
  </main>
</template>

<script>

export default {
    name: 'Main',
    props: {
        movies: Array,
        tv: Array,
    },
    computed:{
        refreshList(){
            return [...this.movies, ...this.tv];
        }
    },
}
</script>

<style scoped lang="scss">
    ol > li{
        margin-bottom: 20px;
    }
    img{
        width: 30px;
    }
</style>