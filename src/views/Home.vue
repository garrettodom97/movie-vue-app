<template>
  <div>
    <h1>{{ greeting }}</h1>
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
    addMovie: function () {
      console.log("Adding movie");
      var params = { title: this.title, year: this.year, plot: this.plot };
      axios
        .post("http://localhost:3000/movies", params)
        .then((response) => {
          console.log(response.data);
          this.movies.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
