<template>
    <div class="card" @click="$emit('getInfo', info)">
        <!-- Poster -->
        <img v-if="info.poster_path" :src="`https://image.tmdb.org/t/p/w${imgWidth}${info.poster_path}`" :alt="info.original_title">
        <img v-else src="../assets/img/img_notfound.jpg" alt="image not found">

        <!-- Info -->
        <Info :info="info" />
       
    </div>
</template>

<script>
// COMPONENTS
import Info from '@/components/Info.vue';

export default {
    name: 'Card',
    components: {
        Info,
    },
    props: {
        info: Object,
        imgWidth: Number,
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
        cursor: pointer;

        &:hover .info{
            opacity: 1;
        }
        // Info Style
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
        }
    }
</style>