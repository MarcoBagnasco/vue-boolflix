<template>
  <header class="flex jc-between ai-center">
      <!-- Logo -->
      <img src="https://fontmeme.com/permalink/210511/c072857f28ffed69c9266a55183f4c20.png" alt="logo">

      <!-- Search Input -->
      <Search @searching="setSearch"/>
  </header>
</template>

<script>
import Search from '@/components/Search.vue'

export default {
    name: 'Header',
    components: {
        Search,
    },
    data(){
        return{
            searchText: '',
        }
    },
    methods: {
        setSearch(text){
            this.searchText = text;
            this.$emit('search', this.searchText)
        }
    }
}
</script>

<style scoped lang="scss">
    header{
        padding: 20px 40px;
        background-color: #181818;
        img{
            width: 200px;
        }
    }
</style>