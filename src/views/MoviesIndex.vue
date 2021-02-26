// Patch Notes: 2/25 img_url key not appearing on response.data

<template>
  <div class="movies-index">
    <div class="jumbotron">
      <h1 class="display-4">Have you seen this movie:</h1>
      <p class="lead">Random Movie Here</p>
      <hr class="my-4">
      <p>This option will show a random movie from the index list.  For now, it just sends you to Home Page</p>
      <a class="btn btn-primary btn-lg" href="/" role="button">Learn more</a>
    </div>
    <br> <br>
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
    
    <div class="row row-cols-1 row-cols-md-2">
      <!-- for loop-->
      <div
        v-for="movie in orderBy(
          filterBy(movies, titleFilter, 'title'),
          orderByFilter
        )"
        v-bind:key="movie.id"
      >
        <!-- card -->
        <div class="col mb-4">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Title: {{ movie.title }}</h5>
              <img src="movie.img_url" class="card-img-top" alt="...">
              <p>Year: {{ movie.year }}</p>
              <p>Plot: {{ movie.plot }}</p>
              <p>Director: {{ movie.director }}</p>
              <p>english: {{ movie.english }}</p>
              <p>genres: {{ movie.genres }}</p>
              <router-link :to="`/movies/${movie.id}`">
                <button type="button" class="btn btn-secondary">Show</button>
              </router-link><br />
              
            </div>
          </div>
        </div>
        <!-- "/movies/:id/edit" -->

      </div>

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