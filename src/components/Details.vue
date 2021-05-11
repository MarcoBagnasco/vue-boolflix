<template>
    <div class="details flex jc-center ai-center">
        <div class="details-box">
            <!-- Exit Icon -->
            <i class="fas fa-times exit" @click="$emit('close')"></i>
            <!-- Info-Box -->
            <div class="info-box flex ai-start">
                <img :src="`https://image.tmdb.org/t/p/w185${details.poster_path}`" :alt="details.original_title">
                <ul class="info">
                    <!-- Title -->
                    <li><strong>Title:</strong> {{details.title !== undefined ? details.title : details.name}}</li>
                    <!-- Original Title -->
                    <li><strong>Original Title:</strong> {{details.original_title !== undefined ? details.original_title : details.original_name}}</li>
                    <!-- Language -->
                    <li>
                        <strong>Language:</strong>
                        <img class="flag" v-if="details.original_language === 'en'" src="../assets/img/en.png" alt="en flag">
                        <img class="flag" v-else-if="details.original_language === 'it'" src="../assets/img/it.png" alt="en flag">
                        <span v-else>{{details.original_language}}</span>
                    </li>
                    <!-- Vote Average -->
                    <li>
                        <strong>Vote Average:</strong>
                        <i v-for="(num, index) in 5"
                        :key="index"
                        class="fas fa-star star"
                        :class="{'full-star': (index + 1) <= Math.floor(details.vote_average / 2),
                        'half-star' : (index + 1) === (Math.ceil(details.vote_average / 2)) && ((details.vote_average / 2) - Math.floor(details.vote_average / 2) > .49)}"></i>
                        {{details.vote_average}}/10
                    </li>
                    <!-- Overview -->
                    <li><strong>Overview:</strong> {{details.overview}}</li>
                </ul>
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

export default {
    name: 'Details',
    props: {
        details: Object,
    },
    data(){
        return{
            reviews: [],
            images: [],
            videos: [],
        }
    },
    created(){
        this.getMoreInfo();
    },
    methods: {
        getMoreInfo(){
            // Call API Movies Reviews
            axios.get(`https://api.themoviedb.org/3/movie/${this.details.id}/reviews`, {
                params: {
                    api_key: 'dabed2596a83196385f10dd2ac69a20d',
                }
            })
            .then(res => {
                this.reviews = res.data.results;
            })
            .catch(err => {
                console.log(err);
            });
            // Call API TV Reviews
            axios.get(`https://api.themoviedb.org/3/tv/${this.details.id}/reviews`, {
                params: {
                    api_key: 'dabed2596a83196385f10dd2ac69a20d',
                }
            })
            .then(res => {
                this.reviews = res.data.results;
            })
            .catch(err => {
                console.log(err);
            });

            // Call API Movies Images
            axios.get(`https://api.themoviedb.org/3/movie/${this.details.id}/images`, {
                params: {
                    api_key: 'dabed2596a83196385f10dd2ac69a20d',
                }
            })
            .then(res => {
                this.images = res.data.backdrops;
            })
            .catch(err => {
                console.log(err);
            });
            // Call API TV Images
            axios.get(`https://api.themoviedb.org/3/tv/${this.details.id}/images`, {
                params: {
                    api_key: 'dabed2596a83196385f10dd2ac69a20d',
                }
            })
            .then(res => {
                this.images = res.data.backdrops;
            })
            .catch(err => {
                console.log(err);
            });

            // Call API Movies Videos
            axios.get(`https://api.themoviedb.org/3/movie/${this.details.id}/videos`, {
                params: {
                    api_key: 'dabed2596a83196385f10dd2ac69a20d',
                }
            })
            .then(res => {
                this.videos = res.data.results;
            })
            .catch(err => {
                console.log(err);
            });
            // Call API TV Videos
            axios.get(`https://api.themoviedb.org/3/tv/${this.details.id}/videos`, {
                params: {
                    api_key: 'dabed2596a83196385f10dd2ac69a20d',
                }
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
            .info{
                width: 70%;
                margin-left: 30px;
                li{
                    margin-bottom: 10px;
                }
            }
            .flag{
                height: 14px;
            }
                    // Stars
            .star{
                position: relative;
                color: #777;
            }
            .full-star{
                color: $red-brand;
            }
            .half-star::after{
                position: absolute;
                top: 0;
                left: 0;
                content: "\f089";
                font-family: "Font Awesome 5 Free"; 
                font-weight: 900; 
                color: $red-brand
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