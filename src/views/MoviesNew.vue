<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h2>Add Movie:</h2>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="newMovieTitle" autofocus placeholder="Enter Title Here" />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="newMoviePlot" placeholder="Enter Plot Here" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="newMovieYear" placeholder="Enter Year Here" />
      </div>
      <input type="submit" class="btn btn-primary" value="Create" />
    </form>

    <!-- <div class="errors" v-for="error in errors" :key="error">
      <p>{{ error }}</p>
    </div> -->
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
      errors: [],
    };
  },
  methods: {
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        plot: this.newMoviePlot,
        year: this.newMovieYear,
      };
      axios
        .post("/api/movies", params)
        .then(response => {
          console.log(response.data);
          this.$router.push("api/movies");
        })
        .catch(error => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
