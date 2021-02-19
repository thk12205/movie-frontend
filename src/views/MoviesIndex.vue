// title: params[:title], year: params[:year], plot: params[:plot], director: params[:director], english: params[:english]

<template>
  <div class="movies-index">
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <p>Director: {{ movie.director }}</p>
      <p>english: {{ movie.english }}</p>
      <p>genres: {{ movie.genres }}</p>
      <!-- "/movies/:id/edit" -->
      <router-link :to="`/movies/${movie.id}`">
        <button>Show</button> </router-link
      ><br />
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    axios.get("/api/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>