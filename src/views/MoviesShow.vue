<template>
  <div class="movies-show">
    <div class="container">
      <h2>{{ movie.title }}</h2>
      <p>{{ movie.year }}</p>
      <p>{{ movie.director }}</p>
      <p>{{ movie.plot }}</p>
      <router-link v-bind:to="`/movies/${movie.id}/edit`"><button>Edit Movie</button></router-link>
      <router-link to="/movies">Back to all movies</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      errors: [],
      movie: {},
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      this.movie = response.data;
    });
  },
};
</script>
