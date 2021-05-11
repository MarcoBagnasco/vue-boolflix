<template>
    <form>
        <button class="search-btn" type="submit" @click.prevent="$emit('searching', searchText)">
            <i class="fas fa-search"></i>
        </button>
        <input v-model="searchText" type="text" name="search" id="search" placeholder="Search Title">
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
// SCSS VARIABLES
@import '../Styles/variables.scss';

    input[type="text"],
    .search-btn{
        height: 2rem;
        padding: 0 10px;
        font-size: 1rem;
        color: $txt-primary-color;
        background-color: $bg-dark;
        border: 1px solid $txt-primary-color;
        outline: none;
        border-radius: 0;

        &:focus{
            background-color: #303030;
        }
    }
    .search-btn{
        border-right: 0;
        cursor: pointer;
    }
    input[type="text"]{
        border-left: 0;

        &::placeholder{
            color: #888;
        }
    }
</style>