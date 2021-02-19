// title: params[:title], year: params[:year], plot: params[:plot], director: params[:director], english: params[:english]

<template>
  <div class="movies-index">
    Search by title: <input type="text" v-model="titleFilter" list="titles" />
    <br />
    <button v-on:click="orderByFilter = 'title'">Order By Title</button>
    <button v-on:click="orderByFilter = 'year'">Order By Title</button>
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">
        {{ movie.title }}
      </option>
    </datalist>
    <div
      v-for="movie in orderBy(
        filterBy(movies, titleFilter, 'title'),
        orderByFilter
      )"
      v-bind:key="movie.id"
    >
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
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "",
      orderByFilter: "",
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