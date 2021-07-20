<template>
  <div>
    <h1>Add a Movie</h1>
    <p>Title:</p>
    <input type="text" v-model="title" />
    <p>Year:</p>
    <input type="text" v-model="year" />
    <p>Plot:</p>
    <input type="text" v-model="plot" />
    <p></p>
    <button v-on:click="addMovie">Add Movie</button>
    <h1>{{ greeting }}</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>{{ movie.title }} - {{ movie.year }}</h2>
      <p>Plot: {{ movie.plot }}</p>
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
