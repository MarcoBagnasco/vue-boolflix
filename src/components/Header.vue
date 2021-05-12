<template>
    <header class="flex jc-between ai-center">
        <!-- Logo -->
        <nav class="flex ai-center">
            <img src="https://fontmeme.com/permalink/210511/c072857f28ffed69c9266a55183f4c20.png" alt="logo">
            <div class="home" @click="$emit('clear')">Home</div>
            <div class="my-list" @click="$emit('showMy')">My List</div>
        </nav>
        <!-- Search Input -->
        <Search @searching="setSearch"/>
    </header>
</template>

<script>
// COMPONENTS
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
        /**
         * Emit search text
         */
        setSearch(text){
            this.searchText = text;
            this.$emit('search', this.searchText)
        }
    }
}
</script>

<style scoped lang="scss">
// SCSS VARIABLES
@import '../Styles/variables.scss';

    header{
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        padding: 20px 40px;
        background: linear-gradient(180deg, rgba(24,24,24,1) 0%, rgba(24,24,24,0.8575805322128851) 24%, rgba(24,24,24,0.7287289915966386) 43%, rgba(24,24,24,0.4990371148459384) 67%, rgba(24,24,24,0) 100%);
        z-index: 10;

        img{
            width: 230px;
        }
        .home,
        .my-list{
            margin: 0 15px;
            cursor: pointer;
        }
    }
</style>