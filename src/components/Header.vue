<template>
  <header>
      <form>
          <input v-model="searchText" type="text" name="search" id="search">
          <button type="submit" @click.prevent="$emit('searchMovie', searchText)">Search</button>
      </form>
  </header>
</template>

<script>
export default {
    name: 'Header',
    data(){
        return{
            searchText: '',
        }
    }
}
</script>

<style scoped lang="scss">

</style>