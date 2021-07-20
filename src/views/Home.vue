<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="createMovie()">Create a new movie!</button>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
      <p>Year: ${{ movie.year }}</p>
      <p>Director: ${{ movie.director }}</p>
      <p>Plot: ${{ movie.plot }}</p>
    </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to movie-vue-app!",
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        this.movies = response.data;
        console.log("All movies:", this.movies);
      });
    },
    createMovie: function () {
      console.log("Creating movie");
      var params = {
        title: "Postcards from the Edge",
        year: 1990,
        plot: "An actress struggles with drug addiction while living in the shadow of her famous mother.",
        director: "Mike Nichols",
        english: true,
      };
      axios
        .post("http://localhost:3000/movies", params)
        .then((response) => {
          console.log("Success!", response.data);
          this.movies.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
