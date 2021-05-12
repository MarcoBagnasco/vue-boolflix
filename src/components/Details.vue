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
            <div class="flex ai-center">
                <div class="trailer" v-if="videos.length !== 0">
                    Watch the <span @click="watchTrailer">Trailer</span>
                    <!-- Video -->
                    <div v-show="showVideo" class="video-box flex jc-center ai-center" @click="watchTrailer">
                        <Video :title="videos[0].key" />
                    </div>
                </div>
                <div v-if="!my.includes(details)" class="add-to-list" @click="$emit('toAdding', details)"><i class="fas fa-plus"></i> Add to My List</div>
                <div v-else class="add-to-list" @click="$emit('toRemove', details)"><i class="fas fa-minus"></i> Remove from My List</div>
            </div>

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
import Video from '@/components/Video.vue';

export default {
    name: 'Details',
    props: {
        details: Object,
        my: Array,
    },
    components: {
        Info,
        Video,
    },
    data(){
        return{
            apiURL: 'https://api.themoviedb.org/3/',
            api_key: 'dabed2596a83196385f10dd2ac69a20d',
            reviews: [],
            images: [],
            videos: [],
            showVideo: false,
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
        },

        /**
         * Toggle video visibility
         */
        watchTrailer(){
            this.showVideo = !this.showVideo;
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
            max-height: 99vh;
            margin: 30px 0;
            padding: 20px;
            background-color: $bg-dark;
            border-radius: 20px;
            overflow: auto;

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
            
            // Trailers
            .trailer{
                margin-top: 10px;
                margin-right: 80px;

                span{
                    color: $red-brand;
                    text-decoration: underline;
                    cursor: pointer;
                }
                
                .video-box{
                    position: fixed;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    background-color: rgba(#000, .7);
                }
            }

            // Add List
            .add-to-list{
                margin-top: 10px;
                cursor: pointer;
                transition: color .3s;

                &:hover{
                    color: $red-brand;
                }
            }

            // Reviews and Images
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

    }
</style>