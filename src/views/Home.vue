<template>
  <div class="home">
      <div :key="movie.id" v-for="movie in movies">
        <movie-component :movie="movie"/>
      </div>
  </div>
</template>

<script>
import Movie from "../components/Movie.vue"
import EventBus from '../eventBus.js'

export default {
  name: 'home',
  components: {
    "movie-component": Movie
  },
  data: () => ({
    movies: [{
      id: 0,
      name: '',
      description: '',
      image: '',
      trailer: '',
      rate: 0,
    }]
  }),
  methods: {
    getMovies() {
      this.$http.get(process.env.VUE_APP_API + 'movies').then(
        success => {
          if (success.status === 200) {
            this.movies = success.body
          }
        }, 
        failure => {
          console.log(failure)
          alert("erro")
        }
      )
    }
  },
  mounted() {
    this.getMovies()
    EventBus.$on('returnHome', () => {
      this.getMovies()
    })
    EventBus.$on('selectCategory', value => {
      this.$http.get(process.env.VUE_APP_API + 'categories' + value).then(
        success => {
          if (success.status === 200) {
            this.movies = success.body.movies
          }
        }, 
        failure => {
          console.log(failure)
          alert("erro")
        }
      )
    })
  }
}

</script>

<style>

.home {
  display: flex;
  flex-flow: wrap;
  margin-left: 12%;
  margin-right: 12%;
}

.home div {
  align-items: center;
}

</style>