<template>
    <div class="card">
        <!-- Poster -->
        <img :src="`https://image.tmdb.org/t/p/w342${info.poster_path}`" alt="">

        <!-- Info -->
        <ul class="info">
            <!-- Title -->
            <li><strong>Title:</strong> {{info.title !== undefined ? info.title : info.name}}</li>
            <!-- Original Title -->
            <li><strong>Original Title:</strong> {{info.original_title !== undefined ? info.original_title : info.original_name}}</li>
            <!-- Language -->
            <li>
                <strong>Language:</strong> 
                <img class="flag" v-if="info.original_language === 'en'" src="../assets/img/en.png" alt="en flag">
                <img class="flag" v-else-if="info.original_language === 'it'" src="../assets/img/it.png" alt="en flag">
                <span v-else>{{info.original_language}}</span>
            </li>
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
    </div>
</template>

<script>
export default {
    name: 'Card',
    props: {
        info: Object,
    },
}
</script>

<style scoped lang="scss">
// SCSS VARIABLES
@import '../Styles/variables.scss';

    .card{
        position: relative;
        width: 100%;
        color: #fff;

        &:hover .info{
            opacity: 1;
        }

        .info{
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            padding: 60px 10px 10px;
            background-color: rgba(#000, .85);
            overflow-y: auto;
            opacity: 0;
            transition: opacity .2s;

            li{
                margin-bottom: 10px;
                
                strong{
                    margin-right: 5px;
                    font-size: 1.2rem;
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
    }
</style>