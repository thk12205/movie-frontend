<template>
  <div class="movies-edit">
    <!-- {{ movie }} -->
    <form v-on:submit.prevent="updateMovie()">
      <h1>Edit Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="movie.title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="movie.year" />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="movie.plot" />
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="movie.director" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
    <button v-on:click="destroyMovie()">Delete</button>
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
  created: function () {
    axios.get(`/api/movies/${this.$route.params.id}`).then((response) => {
      this.movie = response.data;
      console.log("Movie Recieved");
      console.log(this.movie);
    });
  },
  methods: {
    updateMovie: function () {
      var params = {
        title: this.movie.title,
        year: this.movie.year,
        plot: this.movie.plot,
        director: this.movie.director,
        english: true,
      };
      axios
        .patch(`api/movies/${this.movie.id}`, params)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/movies/${this.movie.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyMovie: function () {
      axios.delete(`api/movies/${this.movie.id}`).then((response) => {
        console.log(response.data);
        this.$router.push("/movies");
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