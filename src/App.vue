<template>
  <button v-for="mood in moodMovies" :key="mood" class="btn btn-xs sm:btn-sm md:btn-md lg:btn-lg  border-1 border-accent mr-2" @click="mood.action">{{ mood.mood}}</button>
  <MoviesComponent :movies="movies"/>
  <div>
    <button @click="previousPage()" class="mx-auto btn border-1 border-accent">Previous page</button>
    {{ page }} / {{ totalPages }}
    <button @click="nextPage()" class="mx-auto btn border-1 border-accent">Next page</button>
  </div>
</template>

<script>
import MoviesComponent from './components/MoviesComponent.vue'

export default {
  name: 'App',
  components: {
    MoviesComponent
  },
  data() {
    return {
      movies: {},
      page: 1,
      selectedId: 28,
      totalPages: 1,
      moodMovies: [
{
          mood: '💪', action: () => this.getSelectedMovies(28), data: this.movies
        },
        {
          mood: '🤣', action:() => this.getSelectedMovies(35), data: this.movies
        },
        {
          mood: '😱', action:() => this.getSelectedMovies(27), data: this.movies
        },
        {
          mood: '🤓', action:() => this.getSelectedMovies(878), data: this.movies
        },
        {
          mood: '😔', action:() => this.getSelectedMovies(18), data: this.movies
        },
        {
          mood: '🧐', action:() => this.getSelectedMovies(80), data: this.movies
        },
        {
          mood: '🦸🏻', action:() => this.getSelectedMovies(12), data: this.movies
        },
        {
          mood: '🖖', action:() => this.getSelectedMovies(16), data: this.movies
        },
        {
          mood: '🤔', action:() => this.getSelectedMovies(99), data: this.movies
        },
        {
          mood: '👶🏻‍‍', action:() => this.getSelectedMovies(10751), data: this.movies
        },
        {
          mood: '👾', action:() => this.getSelectedMovies(14), data: this.movies
        },
        {
          mood: '🏛', action:() => this.getSelectedMovies(36), data: this.movies
        },
        {
          mood: '🤠', action:() => this.getSelectedMovies(37), data: this.movies
        },
        {
          mood: '🔫', action:() => this.getSelectedMovies(10752), data: this.movies
        },
        {
          mood: '❓', action:() => this.getSelectedMovies(9648), data: this.movies
        },
        {
          mood: '🥰', action:() => this.getSelectedMovies(10749), data: this.movies
        },
        {
          mood: '🎸', action:() => this.getSelectedMovies(10402), data: this.movies
        },
        {
          mood: '🔪', action:() => this.getSelectedMovies(53), data: this.movies
        },
        {
          mood: '👍', action:() => this.getMovies(), data: this.movies
        }
      ]
    }
  },
  mounted() {
    this.getMovies(28)
  },
  methods: {
    getMovies() {
      this.axios.get(`${process.env.VUE_APP_API_URL}/discover/movie?api_key=${process.env.VUE_APP_SECRET_KEY}&language=fr-FR&sort_by=popularity.desc&include_adult=false&page=${this.page}`)
        .then(response => {
          this.movies = response.data.results
          this.totalPages = response.data.total_pages
        })
        .catch(error => {
          console.log(error)
        })
    },
    getSelectedMovies(id) {
      this.selectedId = id
      this.axios.get(`${process.env.VUE_APP_API_URL}/discover/movie?api_key=${process.env.VUE_APP_SECRET_KEY}&with_genres=${id}&language=fr-FR&include_adult=false&page=${this.page}`)
        .then(response => {
          this.movies = response.data.results
          this.totalPages = response.data.total_pages
        })
        .catch(error => {
          console.log(error)
        })
    },
    nextPage() {
      this.page++
      this.getSelectedMovies(this.selectedId)
      document.body.scrollTop = 0;
      document.documentElement.scrollTop = 0;
    },
    previousPage() {
      if(this.page > 1) {
        this.page--
        this.getSelectedMovies(this.selectedId)
        document.body.scrollTop = 0;
        document.documentElement.scrollTop = 0;
      }
    }
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
