<template>
    <div class="details flex jc-center ai-center">
        <div class="details-box">
            <!-- Exit Icon -->
            <i class="fas fa-times exit" @click="$emit('close')"></i>

            <!-- Info-Box -->
            <div class="info-box flex ai-start">
                <!-- Poster -->
                <img :src="`https://image.tmdb.org/t/p/w185${details.poster_path}`" :alt="details.original_title">
                <!-- Info -->
                <Info :info="details" />
            </div>
            
            <!-- Trailer -->
            <div class="trailer" v-if="videos.length !== 0">Watch the <a :href="`https://www.youtube.com/watch?v=${videos[0].key}`" target="_blank">Trailer</a></div>

            <!-- Reviews -->
            <h2>Reviews</h2>
            <div class="reviews">
                <div class="review" v-for="item in reviews" :key="item.id">
                    <h4>{{item.author}}</h4>
                    {{item.content}}
                </div>
            </div>
            <!-- Images -->
            <h2>Images</h2>
            <div class="images">
                <img v-for="(item,index) in images" :key="index" :src="`https://image.tmdb.org/t/p/w300${item.file_path}`" alt="">
            </div>

        </div>
    </div>
</template>

<script>
// AXIOS
import axios from 'axios';

// COMPONENTS
import Info from '@/components/Info.vue';

export default {
    name: 'Details',
    props: {
        details: Object,
    },
    components: {
        Info,
    },
    data(){
        return{
            apiURL: 'https://api.themoviedb.org/3/',
            api_key: 'dabed2596a83196385f10dd2ac69a20d',
            reviews: [],
            images: [],
            videos: [],
        }
    },
    created(){
        this.getMoreInfo();
    },
    methods: {
        /**
         * Get Reviews, Images and Videos
         */
        getMoreInfo(){
            const apiParams = {
                api_key: this.api_key,
            }
            // Call API Movies Reviews
            axios.get(`${this.apiURL}movie/${this.details.id}/reviews`, {
                params: apiParams,
            })
            .then(res => {
                this.reviews = res.data.results;
            })
            .catch(err => {
                console.log(err);
            });
            // Call API TV Reviews
            axios.get(`${this.apiURL}tv/${this.details.id}/reviews`, {
                params: apiParams,
            })
            .then(res => {
                this.reviews = res.data.results;
            })
            .catch(err => {
                console.log(err);
            });

            // Call API Movies Images
            axios.get(`${this.apiURL}movie/${this.details.id}/images`, {
                params: apiParams,
            })
            .then(res => {
                this.images = res.data.backdrops;
            })
            .catch(err => {
                console.log(err);
            });
            // Call API TV Images
            axios.get(`${this.apiURL}tv/${this.details.id}/images`, {
                params: apiParams,
            })
            .then(res => {
                this.images = res.data.backdrops;
            })
            .catch(err => {
                console.log(err);
            });

            // Call API Movies Videos
            axios.get(`${this.apiURL}movie/${this.details.id}/videos`, {
                params: apiParams,
            })
            .then(res => {
                this.videos = res.data.results;
            })
            .catch(err => {
                console.log(err);
            });
            // Call API TV Videos
            axios.get(`${this.apiURL}tv/${this.details.id}/videos`, {
                params: apiParams,
            })
            .then(res => {
                this.videos = res.data.results;
            })
            .catch(err => {
                console.log(err);
            });
        }
    }
}
</script>

<style scoped lang="scss">
// SCSS VARIABLES
@import '../Styles/variables.scss';

    .details{
        position: fixed;
        top: 0;
        left: 0;
        height: 100vh;
        width: 100%;
        background-color: rgba(#000, .6);
        z-index: 20;

        .details-box{
            position: relative;
            width: 55%;
            margin: 30px 0;
            padding: 20px;
            background-color: $bg-dark;
            border-radius: 20px;
            overflow: hidden;

            .exit{
                position: absolute;
                top: 10px;
                right: 15px;
                font-size: 1.4rem;
                color: rgba(#fff, .4);
                cursor: pointer;
                transition: color .2s;

                &:hover{
                    color: #fff;
                }
            }

            // Info Style
            .info{
                width: 70%;
                margin-left: 30px;
            }
        }
        .trailer{
            margin-top: 10px;
            a{
                color: $red-brand
            }
        }

        h2{
            margin-top: 20px;
        }
        .reviews,
        .images{
            height: 200px;
            margin: 10px;
            overflow-y: auto;
            h4{
                margin-bottom: 5px;
                font-size: 1.3rem;
                text-decoration: underline;
            }
            .review{
                margin: 15px 5px;
            }
            img{
                margin: 10px;
            }
        }
    }
</style>