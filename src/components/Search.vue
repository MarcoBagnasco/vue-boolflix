<template>
    <form>
        <button class="search-btn" type="submit" @click.prevent="$emit('searching', searchText)">
            <i class="fas fa-search"></i>
        </button>
        <input v-model="searchText" type="text" name="search" id="search">
    </form>
</template>

<script>
export default {
    name: 'Search',
    data(){
        return {
            searchText: '',
        }
    }
}
</script>

<style scoped lang="scss">
    input[type="text"],
    .search-btn{
        height: 1.5rem;
        padding: 0 10px;
        color: #fff;
        background-color: #181818;
        border: 1px solid #fff;
        outline: none;
        border-radius: 0;

        &:focus{
            background-color: #333;
        }
    }
    .search-btn{
        border-right: 0;
        cursor: pointer;
    }
    input[type="text"]{
        border-left: 0;
    }
</style>