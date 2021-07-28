<template>
  <div>
    <div class="row row-cols-1 row-cols-md-2 g-4">
      <div class="col">
        <div class="card">
          <img :src="movies[0].image" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{ movies[0].title }} - {{ movies[0].year }}</h5>
            <p class="card-text">
              {{ movies[0].plot }}
            </p>
          </div>
        </div>
      </div>
      <div class="col">
        <div class="card">
          <img :src="movies[1].image" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{ movies[1].title }} - {{ movies[1].year }}</h5>
            <p class="card-text">
              {{ movies[1].plot }}
            </p>
          </div>
        </div>
      </div>
      <div class="col">
        <div class="card">
          <img :src="movies[2].image" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{ movies[2].title }} - {{ movies[2].year }}</h5>
            <p class="card-text">
              {{ movies[2].plot }}
            </p>
          </div>
        </div>
      </div>
      <div class="col">
        <div class="card">
          <img :src="movies[3].image" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{ movies[3].title }} - {{ movies[3].year }}</h5>
            <p class="card-text">
              {{ movies[3].plot }}
            </p>
          </div>
        </div>
      </div>
    </div>

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
