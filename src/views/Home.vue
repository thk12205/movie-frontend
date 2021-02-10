<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- movie data fields -->
    Title: <input type="text" v-model="newMovieTitle"/><br>
    Year: <input type="text" v-model="newMovieYear"/><br>
    Plot: <input type="text" v-model="newMoviePlot"/><br>
    Director: <input type="text" v-model="newMovieDirector"/><br>
    <!-- English: (true/false) <input type="text" v-model="newMovieEnglish"/><br> -->
    <!-- button to add movie -->
    <button v-on:click="createMovie()">Create Movie</button>
    <div v-for="movie in movies" v-bind:key = "movie.id">
      <h1> {{movie.title}} </h1>
      Release Year: {{movie.year}} <br>
      Plot: {{movie.plot}} <br>
      Director: {{movie.director}} <br>
      <!-- Genres: <div v-for="genre in movie.genres" v-bind:key = "movie.id"> <br> -->
      Genres: {{movie.genres}} <br>
    </div>
  </div>
</template>
<style></style>



<script>
import axios from "axios";
//setup backend
//open movie app
//find indexMovies response and save json view outputs
//Home.vue add the ability to see all movies
//create data
//add fake movies array with proper params
//edit message
//create webpage
//generate title
//generate the for loop
//generate the movie in movies loop
//check if webpage shows
//in created, add the function indexMovie
//pull response from axios.get()
//test
//fill the rest
// CORS Reverse

//add createMovie function in methods
//add input line for movie fields
//title, year, plot, director, english

//JSON Output
// "id": 8,
// "title": "sharknado",
// "year": 2005,
// "plot": "plotheavy",
// "director": "Woopie Goldberg",
// "english": true,
// "genres": [
//   "Action",
//   "Fantasy"
// ]

export default {
  data: function () {
    return {
      message: "Movies!!",
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieEnglish: "",
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/movies/").then((response) => {
        this.movies = response.data;
      });
    },
    createMovie: function () {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        english: true, //hardcoded boolean
        // title: "Around the World in 80 Days",
        // year: 2015,
        // plot:
        //   "Man travels around the world in 80 days to win a bet and prove his scientific point",
        // director: "Je",
        // english: true, //hardcode
      };
      axios
        .post("/api/movies/", params)
        .then((response) => {
          console.log("Sanity Test");
          this.movies.push(response.data);
        })
        .catch((error) => {
          console.log("Sanity Test, Error-style");
          console.log(error.response.data.errors);
        });
    },
  },
};

// title: "Around the World in 80 Days",
// year: 2015,
// plot:
//   "Man travels around the world in 80 days to win a bet and prove his scientific point",
// director: "Jeff Goldblum",
// english: true, //hardcode
</script>

