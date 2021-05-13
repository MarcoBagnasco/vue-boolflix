<template>
    <div class="list-section">
        <!-- SECTION HEADER -->
        <div class="flex ai-center">
            <h2>{{title}}</h2>
            <!-- Genre Filter -->
            <GenreFilter @chooseGenre="setGenre"/>
        </div>

        <!-- TITLE LIST -->
        <div class="list-box">
            <ul class="movies-list flex ai-center">
                <!-- CARD -->
                <li v-for="item in arrayList" :key="item.id">
                        <Card :info="item" :imgWidth="154" @getInfo="sendInfo"/>
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
    name: 'SmallList',
    components:{
        Card,
        GenreFilter,
    },
    props: {
        title: String,
        list: Array,
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
    methods:{
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
            ul{
                margin-top: 25px;
                overflow-x: auto;

                li{
                    width: 154px;
                    margin: 0 5px;
                    font-size: 0.7em;
                }
            }
        }
    }

</style>