<template>
  <div id="movies">
    <div class="movie-container" v-for="movie in movies" :key="movie.imdbID">
      <div class="image-container">
        <img :src="movie.Poster === 'N/A' ? 'img/default.jpg' : movie.Poster" />
      </div>
      <div class="info">
        <h3 class="title">{{ movie.Title }}</h3>
        <p>{{ movie.Type + ' / ' + movie.Year }}</p>
        <div class="action_container">
          <span
            @click="favoriteMovieTrigger(movie)"
            :class="{ 'isFavourite': movie.favorite }"
          >
            <i class="fa fa-heart "></i>
          </span>
          <a
            target="_blank"
            class="button"
            :href="`https://www.imdb.com/title/${movie.imdbID}/`"
            >IMDB ></a
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['movies'],
  methods: {
    favoriteMovieTrigger(movie) {
      const favoriteMovie = { ...movie, favorite: true };
      this.$emit('favoriteMovieTrigger', favoriteMovie);
    },
  },
};
</script>

<style>
.isFavourite > i {
  color: red !important;
}
</style>
