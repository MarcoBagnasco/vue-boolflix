<template>
    <ul class="info">
            <!-- Title -->
            <li><strong>Title:</strong> {{info.title !== undefined ? info.title : info.name}}</li>
            <!-- Original Title -->
            <li><strong>Original Title:</strong> {{info.original_title !== undefined ? info.original_title : info.original_name}}</li>
            <!-- Language -->
            <li>
                <strong>Language:</strong> 
                <img class="flag" v-if="languageFlag.includes(info.original_language)" :src="require(`../assets/img/${info.original_language}.png`)" :alt="info.original_language">
                <span v-else>{{info.original_language}}</span>
            </li>
            <li><strong>Release Date:</strong> {{info.release_date}}</li>
            <!-- Vote Average -->
            <li>
                <strong>Vote Average:</strong>
                <i v-for="(num, index) in 5" 
                :key="index" 
                class="fas fa-star star" 
                :class="{'full-star': (index + 1) <= Math.floor(info.vote_average / 2),
                'half-star' : (index + 1) === (Math.ceil(info.vote_average / 2)) && ((info.vote_average / 2) - Math.floor(info.vote_average / 2) > .49)}"></i>
                {{info.vote_average}}/10
            </li>
            <!-- Overview -->
            <li><strong>Overview:</strong> {{info.overview}}</li>
        </ul>
</template>

<script>
export default {
    name: 'Info',
    props: {
        info: Object,
    },
    data(){
        return{
            languageFlag: ['en','it'],
        }
    }
}
</script>

<style scoped lang="scss">
// SCSS VARIABLES
@import '../Styles/variables.scss';

    .info{
        li{
            margin-bottom: 10px;
            
            strong{
                margin-right: 5px;
                font-size: 1.2em;
                text-decoration: underline;
            }

            .flag{
                height: 14px;
            }
        }
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
</style>