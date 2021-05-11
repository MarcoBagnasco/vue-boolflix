<template>
    <main>
        <!-- MOVIES LIST -->
        <ListSection :title="'Movies'" :list="movies"/>

        <!-- TV LIST -->
        <ListSection :title="'TV Shows'" :list="tv"/>
    </main>
</template>

<script>
// COMPONENTS
import ListSection from '@/components/ListSection.vue';

export default {
    name: 'Main',
    components: {
        ListSection,
    },
    props: {
        movies: Array,
        tv: Array,
    },
}
</script>

<style scoped lang="scss">
// SCSS VARIABLES
@import '../Styles/variables.scss';

    main{
        padding: 0 20px;
    }
</style>