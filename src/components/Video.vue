<template>
    <iframe class="video" width="560" height="315" :src="`https://www.youtube.com/embed/${title}`" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</template>

<script>
export default {
    name: 'Video',
    props: {
        title: String,
    }
}
</script>