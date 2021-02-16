<template>
  <div class="movies-index">
    <h1>Movies</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>{{ movie.title }}</h2>
      <p>{{ movie.plot }}</p>
      <p>Directed by: {{ movie.director }}</p>
      <p>{{ movie.year }}</p>
      <router-link :to="`/movies/${movie.id}`">More Info</router-link>
      <!-- <router-link :to="`/movies/${movie.id}/edit`"><button>Edit</button></router-link> -->
      <br />
    </div>
  </div>
</template>
<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      movies: [],
    };
  },
  created: function() {
    axios
      .get("/api/movies")
      .then(response => {
        console.log(response.data);
        this.movies = response.data;
      })
      .catch(error => {
        console.log(error.response.data);
      });
  },
  methods: {},
  // indexMovies: function() {
};
</script>
