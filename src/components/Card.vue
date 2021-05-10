<template>
    <div class="card">
        <!-- Poster -->
        <img :src="`https://image.tmdb.org/t/p/w185${info.poster_path}`" alt="">

        <!-- Info -->
        <ul>
            <!-- Title -->
            <li><strong>Title: </strong>{{info.title !== undefined ? info.title : info.name}}</li>
            <!-- Original Title -->
            <li><strong>Original Title: </strong>{{info.original_title !== undefined ? info.original_title : info.original_name}}</li>
            <!-- Language -->
            <li>
                <strong>Language: </strong>
                <img class="flag" v-if="info.original_language === 'en'" src="../assets/img/en.png" alt="en flag">
                <img class="flag" v-else-if="info.original_language === 'it'" src="../assets/img/it.png" alt="en flag">
                <span v-else>{{info.original_language}}</span>
            </li>
            <!-- Vote Average -->
            <li>
                <strong>Vote Average: </strong>{{info.vote_average}}/10
                <i v-for="(num, index) in Math.round(info.vote_average / 2)" :key="index" class="fas fa-star"></i>
                <i v-for="(num, index) in 5 - Math.round(info.vote_average / 2)" :key="index" class="far fa-star"></i>
                {{(info.vote_average / 2)}}
            </li>
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
    ol > li{
        margin-bottom: 20px;
    }
    .flag{
        width: 30px;
    }
</style>