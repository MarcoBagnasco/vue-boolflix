<template>
    <div class="list-section">
        <div class="flex ai-center">
            <h2>{{title}}</h2>
            <span class="scroll" v-show="scrollID === 0" @click="scroll">Start Scroll</span>
        </div>

        <!-- TITLE LIST -->
        <div class="list-box" ref="bau">
            <ul class="movies-list flex ai-center" tabindex="0" @focus="stopScroll">
                <!-- CARD -->
                <li v-for="item in list" :key="item.id" >
                    <Card :info="item" :imgWidth="342" @getInfo="sendInfo"/>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
// COMPONENTS
import Card from '@/components/Card.vue';

export default {
    name: 'ScrollList',
    components:{
        Card,
    },
    props: {
        title: String,
        list: Array,
    },
    data(){
        return{
            details: {},
            scrollID: 0,
            left: true,
        }
    },
    created(){
        this.scroll();
    },
    methods: {
        /**
         * Scroll the list
         */
        scroll(){
            this.scrollID = setInterval(() => {
                if(this.$refs.bau.scrollLeft === 0){
                    this.left = true;
                }
                if(this.$refs.bau.scrollLeft === 5200){
                    this.left = false;
                }
                if(this.left){
                    this.$refs.bau.scrollLeft += 1;
                } else {
                    this.$refs.bau.scrollLeft -= 1;
                }
            }, 10);
        },

        /**
         * Stop scroll the list
         */
        stopScroll(){
            clearInterval(this.scrollID);
            this.scrollID = 0;
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

        .scroll{
            margin-left: 20px;
            cursor: pointer;
            transition: color .2s;

            &:hover{
                color: $red-brand;
            }
        }
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
    }
</style>