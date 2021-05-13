<template>
    <div class="genre">
        Filter by Genre
        <i v-if="!open" class="fas fa-chevron-down" @click="openMenu"></i>
        <i v-else class="fas fa-chevron-up" @click="openMenu"></i>
        <!-- Genre Menu -->
        <ul v-show="open" class="genre-list flex">
            <li @click="takeGenre('', null); openMenu()">All</li>
            <li v-for="(item, index) in genres" :key="index" @click="takeGenre(item.name, item.id); openMenu()">{{item.name}}</li>
        </ul>
        <!-- Genre Name -->
        <span v-show="genreName.length" class="genre-name">{{genreName}}<i class="fas fa-times-circle delete" @click="takeGenre('', null)"></i></span>
    </div>
</template> 

<script>
// AXIOS
import axios from 'axios';

export default {
    name: 'GenreFilter',
    data(){
        return {
            apiURL: 'https://api.themoviedb.org/3/',
            api_key: 'dabed2596a83196385f10dd2ac69a20d',
            genres: [],
            open: false,
            genreName: '',
        }
    },
    created(){
        this.getGenres();
    },
    methods: {
        /**
         * Call API for genres
         */
        getGenres(){
            const apiParams = {
                api_key: this.api_key,
            }   
            axios.get(`${this.apiURL}genre/movie/list`, {
                params: apiParams,
            })
            .then(res => {
                this.genres = res.data.genres;
            })
            .catch(err => {
                console.log(err);
            });
        },

        /**
         * Open/Close genre menu
         */
        openMenu(){
            this.open = !this.open;
        },

        /**
         * Take genre name and id
         */
        takeGenre(name, id){
            this.genreName = name;
            this.$emit('chooseGenre', id);
        }

    }
}
</script>

<style scoped lang="scss">
// SCSS VARIABLES
@import '../Styles/variables.scss';

    .genre{
        position: relative;
        margin-left: 50px;

        i{
            margin-left: 10px;
            cursor: pointer;
        }
        .genre-list{
            flex-wrap: wrap;
            position: absolute;
            top: 100%;
            left: 0;
            width: 400px;
            padding: 10px;
            background-color: $bg-dark;
            z-index: 1;

            li{
                width: calc(50% - 10px);
                margin-bottom: 5px;
                cursor: pointer;
            }
        }

        .genre-name{
            margin-left: 30px;

            .delete{
                position: relative;
                bottom: 10px;
                font-size: 0.6em;
                transition: color .3s;
                &:hover{
                    color: $red-brand
                }
            }
        }
    }
</style>