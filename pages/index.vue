<template>
  <div class="home">
<Hero-pics/>
<!-- Movie -->
<div class="container movies">
  <div id="movie-grid" class="movie-grid">
   <div v-for="(movie, index) in movies" :key='index' class="movie">
     <div class="movie-img">
       <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="">
    
     <p class="review">
       {{ movie.vote_average}}
     </p>
     <p class="overview">
       {{ movie.overview}}
     </p>
      </div>
      <div class="info">
        <p class="title">
          {{ movie.title.slice(0, 25) }} <span v-if="movie.title.length > 25">...</span>
        </p>
        <p class="release">
          Released:
          {{
            new Date(movie.release_date.toLocaleString('eng-us', {
              month: 'long',
              day: 'numeric',
              year:'numeric'
            }))
          }}
        </p>
      </div>

   </div>
  </div>
</div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'IndexPage',
  data(){
    return{
      movies: []
    }
  },
  async fetch(){
     await this.getMovies()
  },
  methods: {
      async getMovies() {
        const data = axios.get(`https://api.themoviedb.org/3/movie/now_playing?api_key=${process.env.VUE_APP_API_KEY}&language=en-US&page=1`)
        const result = await data
       result.data.results.forEach(movie => {
         this.movies.push(movie)
       })
       console.log(this.movies);
      }
      
  }
}
</script>
