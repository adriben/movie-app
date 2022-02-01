<template>
<Loading-spiner v-if="$fetchState.pending"/>
    <div v-else class="container single-movie">
        <h1>{{ this.movie.title }}</h1>
    </div>
</template>
<script >
import axios from 'axios';

export default {
    name: 'single-movie',
    data(){
        return {
            movie: {},
            apiKey: process.env.VUE_APP_API_KEY,

        }
    },
    async fetch(){
        await this.getSingleMovie()

    },
    fetchDelay: 1000,

    methods: {
        async getSingleMovie() {
        
        const data = axios.get(`https://api.themoviedb.org/3/movie/${this.$route.movieid}?api_key=65edaf62da630f3d1bc494487dfe9722&language=en-US`)
        
        const result = await data
        this.movie = result.data
        console.log(result);
        }

    }
}

</script>

<style lang="scss" scoped>

</style>