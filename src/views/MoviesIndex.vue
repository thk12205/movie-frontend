// title: params[:title], year: params[:year], plot: params[:plot], director: params[:director], english: params[:english]

<template>
  <div class="movies-index">
    Search by title: <input type="text" v-model="titleFilter" list="titles" />
    <br />
    <h3>Order By:</h3>
    <input
      type="radio"
      id="title"
      name="orderFilter"
      value="title"
      v-on:change="orderByFilter = 'title'"
    />
    <label for="title">Title</label><br />
    <input
      type="radio"
      id="year"
      name="orderFilter"
      value="year"
      v-on:change="orderByFilter = 'year'"
    />
    <label for="year">Year</label><br />
    <!--  -->
    <input
      type="radio"
      id="director"
      name="orderFilter"
      value="director"
      v-on:change="orderByFilter = 'director'"
    />
    <label for="director">Director</label> <br />
    <!--  -->
    <input
      type="radio"
      id="ID"
      name="orderFilter"
      value="ID"
      v-on:change="orderByFilter = 'id'"
    />
    <label for="ID">ID</label>

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