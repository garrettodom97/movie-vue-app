<template>
  <div>
    Search:
    <input v-model="keyword" />
    <div class="row row-cols-1 row-cols-md-2 g-4">
      <div class="col" v-for="movie in filterBy(movies, keyword, 'title', 'plot', 'year', 'director')" :key="movie.id">
        <router-link :to="`/movies/${movie.id}`">
          <div class="card">
            <img :src="movie.image" class="card-img-top" alt="..." />
            <div class="card-body">
              <h5 class="card-title">{{ movie.title }} - {{ movie.year }}</h5>
              <p class="card-text">
                {{ movie.plot }}
              </p>
            </div>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],

  data: function () {
    return {
      greeting: "Welcome to the Movie App",
      movies: [],
      title: "Title",
      year: 1900,
      plot: "Plot",
      keyword: "",
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
