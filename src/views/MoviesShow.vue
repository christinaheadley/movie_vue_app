//
<template>
  <div class="movies-show">
    <h1>{{ movie.title }}</h1>
    <p>{{ movie.plot }}</p>

    <p>Directed by: {{ movie.director }}</p>

    <p>{{ movie.year }}</p>
    <!-- {{ movie.id }} -->

    <br />
  </div>
</template>
//
<style></style>

//
<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {},
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      this.movie = response.data;
      console.log(response.data); //OR (this.movie)-- at this point are equivalent
    });
    // axios
    //   .get(`/api/movies/${this.$route.params.id}`) //vue syntax
    //   .then(response => {
    //     this.movie = response.data;
    //     console.log(this.movie);
    //   });
    // .catch(error => {
    //   console.log(error.response.data);
    // });
  },
  methods: {},
};
</script>
