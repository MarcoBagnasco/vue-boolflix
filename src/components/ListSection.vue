<template>
    <div class="list-section">
        <!-- SECTION HEADER -->
        <div class="flex ai-center jc-between">
            <div class="left flex ai-center">
                <h2>{{title}}</h2>
                <!-- Genre Filter -->
                <GenreFilter @chooseGenre="setGenre"/>
            </div>
            <div v-show="title != 'My List'" class="results">Results for "{{search}}"</div>
        </div>

        <!-- TITLE LIST -->
        <div class="list-box">
            <ul class="movies-list flex ai-center">
                <!-- CARD -->
                <li v-for="item in arrayList" :key="item.id">
                    <Card :info="item" :imgWidth="342" @getInfo="sendInfo"/>
                </li>
            </ul>
            
            <div v-show="!arrayList.length">No title for this genre</div>
        </div>
    </div>
</template>

<script>
// COMPONENTS
import Card from '@/components/Card.vue';
import GenreFilter from '@/components/GenreFilter.vue';


export default {
    name: 'ListSection',
    components:{
        Card,
        GenreFilter,
    },
    props: {
        title: String,
        list: Array,
        search: String,
    },
    data(){
        return{
            details: {},
            idGenre: null,
        }
    },
    computed: {
        /**
         * Array to loop
         */
        arrayList(){
            if(this.idGenre === null){
                return this.list;
            } else {
                return this.list.filter(item => item.genre_ids.includes(this.idGenre));
            }
        }
    },
    methods: {
        /**
         * Set genre
         */
        setGenre(id){
            this.idGenre = id;
        },

        /**
         * Emit details
         */
        sendInfo(obj){
            this.details = obj;
            this.$emit('getDetails', this.details)
        }
    }
}
</script>

<style scoped lang="scss">
// SCSS VARIABLES
@import '../Styles/variables.scss';

    .list-section{
        margin: 30px 0;
        padding: 30px;
        background-color: $bg-dark-soft;

        .list-box{
            overflow-x: auto;

            ul{
                margin-top: 25px;

                li{
                    width: 342px;
                    margin: 0 5px;
                }
            }
        }

        .results{
            margin-right: 60px;
            font-size: 1.2em;
            font-weight: bold;
        }
    }
</style>