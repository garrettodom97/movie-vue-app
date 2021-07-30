<template>
  <div>
    <form v-on:submit.prevent="addMovie()">
      <h1>Add a Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        <label>Director:</label>
        <input type="text" v-model="newMovieParams.director" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="newMovieParams.plot" />
        <small>{{ 100 - newMovieParams.plot.length }} characters remaining</small>
      </div>
      <div>
        <label>English?:</label>
        <input type="checkbox" value="true" v-model="newMovieParams.english" />
      </div>
      <input v-if="newMovieParams.plot.length < 100" type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newMovieParams: { plot: "" },
      errors: {},
    };
  },
  methods: {
    addMovie: function () {
      if (this.newMovieParams.english == "true") {
        this.newMovieParams.english = true;
      } else {
        this.newMovieParams.english = false;
      }
      console.log(this.newMovieParams.english);
      axios
        .post("http://localhost:3000/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
