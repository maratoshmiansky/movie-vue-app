<template>
  <div class="allmovies">
    <div v-for="movie in movies" :key="movie.id">
      <router-link v-bind:to="`/movies/${movie.id}`">
        <h2>Title: {{ movie.title }}</h2>
        <p>Year: {{ movie.year }}</p>
        <p>Director: {{ movie.director }}</p>
        <p>Plot: {{ movie.plot }}</p>
      </router-link>
      <button>More info!</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Here are movies!",
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/movies").then((response) => {
        this.movies = response.data;
        console.log("All movies:", this.movies);
      });
    },
  },
};
</script>
