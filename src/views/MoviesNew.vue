<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input
          type="text"
          class="form-control"
          v-model="movie.title"
          placeholder="Seven Samurai"
        />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input
          type="text"
          class="form-control"
          v-model="movie.year"
          placeholder="1954"
        />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input
          type="text"
          class="form-control"
          v-model="movie.plot"
          placeholder="What's the use of worrying about your beard when your head's about to be taken?"
        />
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input
          type="text"
          class="form-control"
          v-model="movie.director"
          placeholder="Akira Kurosawa"
        />
      </div>
      <div>
        <input type="submit" class="btn btn-primary" value="Submit" />
      </div>
    </form>
    <button v-on:click="testMethod()"></button>
  </div>
</template>


      // <h2>Title: {{ movie.title }}</h2>
      // <p>Year: {{ movie.year }}</p>
      // <p>Plot: {{ movie.plot }}</p>
      // <p>Director: {{ movie.director }}</p>
      // <p>english: {{ movie.english }}</p> not required
      // <p>genres: {{ movie.genres }}</p>  not required 

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      errors: [],
      movie: {},
    };
  },
  methods: {
    createMovie: function () {
      var params = {
        title: this.movie.title,
        year: this.movie.year,
        plot: this.movie.plot,
        director: this.movie.director,
        english: true,
      };
      axios
        .post("api/movies", params)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    // title: params[:title], year: params[:year], plot: params[:plot], director: params[:director], english: params[:english]
    // submit: function () {
    //   var params = {
    //     email: this.email,
    //     password: this.password,
    //   };
    //   axios
    //     .post("/api/sessions", params)
    //     .then((response) => {
    //       axios.defaults.headers.common["Authorization"] =
    //         "Bearer " + response.data.jwt;
    //       localStorage.setItem("jwt", response.data.jwt);
    //       this.$router.push("/");
    //     })
    //     .catch((error) => {
    //       console.log(error.response);
    //       this.errors = ["Invalid email or password."];
    //       this.email = "";
    //       this.password = "";
    //     });
    // },
    testMethod: function () {
      console.log(this.movie);
    },
  },
};
</script>