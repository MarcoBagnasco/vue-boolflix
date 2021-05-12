<template>
    <div class="list-section">
        <h2>{{title}}</h2>

        <!-- TITLE LIST -->
        <div class="list-box">
            <ul class="movies-list flex ai-center">
                <!-- CARD -->
                <li v-for="item in list" :key="item.id">
                    <Card :info="item" @getInfo="sendInfo"/>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
// COMPONENTS
import Card from '@/components/Card.vue';

export default {
    name: 'ListSection',
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
        }
    },
    methods: {
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
    }
</style>