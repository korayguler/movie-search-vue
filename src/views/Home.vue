<template>
  <div class="home">
    <movie-search @searchTrigger="searchMovie" />
    <movie-card :movies="searchResult" @favoriteMovieTrigger="favoriteMovie" />
  </div>
</template>

<script>
import Axios from 'axios';
import MovieSearch from '@/components/MovieSearch';
import MovieCard from '@/components/MovieCard';
export default {
  components: {
    MovieSearch,
    MovieCard,
  },
  data() {
    return {
      searchResult: [],
      omdb: `http://www.omdbapi.com/?apikey=${process.env.VUE_APP_API_KEY}`,
    };
  },
  methods: {
    async searchMovie(searchValue) {
      if (!searchValue) return;

      const response = await Axios.post(`${this.omdb}&s=${searchValue}`);
      if (response.status == 200) {
        this.searchResult = response.data.Search.map((m) => ({
          ...m,
          favorite: false,
        }));
      }
    },
    async favoriteMovie(movie) {
      if (!movie) return;

      this.searchResult.map((m) => {
        if (m.imdbID === movie.imdbID) {
          m.favorite = true;
        }
      });

      const request = await Axios.get('http://localhost:3000/favorites');

      if (request.status === 200) {
        let search = request.data.find((m) => m.imdbID == movie.imdbID);
        if (search) return;
        else {
          const request = await Axios.post(
            'http://localhost:3000/favorites',
            movie,
          );
        }
      }
    },
  },
};
</script>

<style>
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
