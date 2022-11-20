<template>
  <div class="flex flex-wrap text-white justify-around px-4 mt-12">
    <div v-for="movie in movies" :key="movie.id" class="card sm:w-1/4 w-1/1 glass mb-6 mr-1">
      <figure class="sm:mt-4 m-4"><img :src="`https://image.tmdb.org/t/p/w154/${movie.poster_path}`" alt="Movie poster"/></figure>
      <div class="card-body">
        <h2 class="card-title flex flex-wrap justify-between"><span>{{ movie.title }}</span> <span>{{ movie.release_date }}</span></h2>
        <div class="rating gap-1 flex mx-auto">
          <input v-for="n in Math.round(movie.vote_average / 2)" :key="n" type="radio" name="rating-3" class="mask mask-heart bg-red-400" />
        </div>
        <p>{{ movie.overview }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MoviesList',
  props: {
    movies: {
      type: Object,
      required: true
    }
  }
}

</script>
