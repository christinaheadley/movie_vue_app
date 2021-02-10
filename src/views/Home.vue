<template>
  <div class="home">
    <h1>Movies</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>{{ movie.title }}</h2>
      <p>{{ movie.plot }}</p>
      <p>Directed by: {{ movie.director }}</p>
      <p>{{ movie.year }}</p>
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
      actors: [],
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("http://localhost:3000/api/movies").then(response => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovies: function() {
      var params = {
        director,
        english,
        genres,
        id,
        plot,
        title,
        year,
      };
      axios
        .post("http://localhost:3000/api/movies".params)
        .then(response => {
          this.movie = response.data;
          this.movies.push(response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
