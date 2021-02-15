<template>
  <div class="home">
    <div>
      <h2>Add Movie:</h2>
      Title:
      <input type="text" v-model="newMovieTitle" />
      <br />
      Plot:
      <input type="text" v-model="newMoviePlot" />
      <br />
      Year:
      <input type="text" v-model="newMovieYear" />
      <br />
      <button v-on:click="createMovie">Add movie</button>
    </div>
    <!-- <div class="errors" v-for="error in errors" :key="error">
      <p>{{ error }}</p>
    </div> -->

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
      movies: [],
      actors: [],
      newMovieTitle: "",
      newMoviePlot: "",
      newMovieYear: "",
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios
        .get("http://localhost:3000/api/movies")
        .then(response => {
          console.log(response.data);
          this.movies = response.data;
        })
        .catch(error => {
          console.log(error.response.data);
        });
    },
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        plot: this.newMoviePlot,
        year: this.newMovieYear,
      };
      axios
        .post("http://localhost:3000/api/movies", params)
        .then(response => {
          this.movies.push(response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
