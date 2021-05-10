<template>
  <main>
      <!-- MOVIES LIST -->
      <ol>
          <li v-for="(item, index) in movies" :key="index">
              <!-- Movie Info -->
              <ul>
                  <li><strong>Title: </strong>{{item.title}}</li>
                  <li><strong>Original Title: </strong>{{item.original_title}}</li>
                  <li><strong>Language: </strong>{{item.original_language}}</li>
                  <li><strong>Vote Average: </strong>{{item.vote_average}}</li>
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
    },
}
</script>

<style scoped lang="scss">
    ol > li{
        margin-bottom: 20px;
    }
</style>