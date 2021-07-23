<template>
  <div>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <router-link :to="`/movies/${movie.id}`">
        <h2>{{ movie.title }} - {{ movie.year }}</h2>
        <p>Plot: {{ movie.plot }}</p>
      </router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      greeting: "Welcome to the Movie App",
      movies: [],
      title: "Title",
      year: 1900,
      plot: "Plot",
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios
        .get("http://localhost:3000/movies")
        .then((response) => {
          console.log(response.data);
          this.movies = response.data;
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
