<template>
  <div class="favorites">
    <movie-card
      :movies="favoriteMovies"
      @favoriteMovieTrigger="removeFromFavorites"
    />
  </div>
</template>

<script>
import Axios from 'axios';
import MovieCard from '@/components/MovieCard';
export default {
  components: {
    MovieCard,
  },
  data() {
    return {
      favoriteMovies: [],
    };
  },
  methods: {
    async initCall() {
      try {
        const response = await Axios.get('http://localhost:3000/favorites');
        if (response.status == 200) this.favoriteMovies = response.data;
      } catch (err) {
        console.log(err);
      }
    },
    async removeFromFavorites(movie) {
      if (!movie.favorite) return;
      try {
        const response = await Axios.delete(
          `http://localhost:3000/favorites/${movie.id}`,
        );
        if (response.status === 200) {
          this.favoriteMovies = this.favoriteMovies.filter(
            (m) => m.id !== movie.id,
          );
        }
      } catch (err) {
        console.log(err);
      }
    },
  },
  mounted() {
    this.initCall();
  },
};
</script>
