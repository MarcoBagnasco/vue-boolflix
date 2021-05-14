<template>
    <form>
        <!-- Search Button -->
        <button class="search-btn pointer" type="submit" @click.prevent="$emit('searching', searchText)">
            <i class="fas fa-search"></i>
        </button>
        <!-- Input -->
        <input v-model.trim="searchText" type="text" name="search" id="search" placeholder="Search Title" @keyup="$emit('searching', searchText)">
        <!-- Cancel Field -->
        <i class="fas fa-times cancel pointer" @click="searchText = ''"></i>
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

    form{
        position: relative;
    }

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
    }

    input[type="text"]{
        padding-right: 30px;
        border-left: 0;

        &::placeholder{
            color: #888;
        }
    }
    
    .cancel{
        position: absolute;
        top: 7px;
        right: 10px;
    }
</style>