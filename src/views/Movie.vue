<template>
  <div class="movie">

    <div id="div1">
      <div id="image">
        <img id="banner" align="left" :src="movie.image">
        <h3 id="rate">{{movie.rate}} / 10</h3>
        <h1 id="name">{{movie.name}}</h1>
        <small id="categories">Categorias: </small>
        <small id="categories" v-for="category in movie.categories" :key="category.id">{{category.name}} </small>
        <h1 id="description">{{movie.description}}</h1>
      </div>
    </div>

    <div id="div2">
      <iframe id="trailer" frameborder="0" allowfullscreen :src="movie.trailer"></iframe>
    </div>

    <h2 class="rec">Recomendados</h2>

    <div id="div3">
        <div id="categorias">
          <div :key="recMovie.id" v-for="recMovie in recMovies">
            <movie-component v-if="recMovie.id != movie.id" :movie="recMovie"/>
          </div>
        </div>
    </div>

  </div>
</template>

<script>
import Movie from "../components/Movie.vue"

export default {
  name: 'movie',
  data: () => ({
    movie: {

    },
    recMovies: [

    ],
    recCounter: 0
  }),
  components: {
    "movie-component": Movie
  },
  methods: {
    loadRecMovies() {
      this.$http.get(process.env.VUE_APP_API + 'categories/' + this.movie.categories[0].id).then(
        success => {
          if (success.status === 200) {
            this.recMovies = success.body.movies.filter((value) => value.id != this.movie.id).slice(0,3)
          }
        }, 
        failure => {
          console.log(failure)
          alert("erro")
        }       
      )
    },
    loadData() {
      this.$http.get(process.env.VUE_APP_API + 'movies/' + this.$route.params.id).then(
        success => {
          if (success.status === 200) {
            this.movie = success.body
            this.loadRecMovies()
            window.scrollTo(0,0);
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
    this.loadData()
  },
  beforeRouteUpdate(to, from, next) {
    next()
    this.loadData()
  }

}

</script>

<style scoped>
#categories {
    color: whitesmoke;
}

.movie {
    text-align: center;
    position: relative;
    height: auto;
}

#rate {
    color: rgb(236, 236, 15);
    text-align: center;
    padding-top: 10px;
}

#name {
    color: whitesmoke;
}

#description {
    color: whitesmoke;
    text-align: justify;
}

#banner {
    width: 100%;
    height: 100%;
    padding-bottom: 15px;
}

#trailer {
    position: relative;
    overflow: auto;
    margin: 0 auto;
    height: 600px;
    width: 900px;
}

#div1 {
    width: 900px;
    margin: 0 auto;
}

.rec {
    position: relative;
    text-align: center;
    color: whitesmoke;
}

#div3 {
    margin: 0 auto;
    width: 900px;
}

#div2 {
    margin-bottom: 50px;
}

#categorias {
  display: flex;
  flex-flow: wrap;
  margin-left: 12%;
  margin-right: 12%;
  width: 100%;
}

#categorias div {
  align-items: center;
}


</style>