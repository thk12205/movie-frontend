<template>
  <div class="movies-show">
    <h2>Title: {{ movie.title }}</h2>
    <p>Year: {{ movie.year }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <p>Director: {{ movie.director }}</p>
    <p>english: {{ movie.english }}</p>
    <p>genres: {{ movie.genres }}</p>
    <router-link :to="`/movies/${movie.id}/edit`">
      <button>Edit Movie</button> </router-link
    ><br />
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: [],
    };
  },
  created: function () {
    axios.get(`/api/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {},
};
</script>