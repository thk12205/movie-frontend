<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/signup">Signup</router-link> |
      <router-link to="/login">Login</router-link> |
      <router-link to="/logout">Logout</router-link> |
      <router-link to="/movies">Movie Index</router-link> |
      <router-link to="/movies/new">New Movie</router-link>
    </div>
    <router-view />
  </div>
</template>

// import MoviesIndex from "../views/MoviesIndex.vue";
// import MoviesNew from "../views/MoviesNew.vue";
// import MoviesShow from "../views/MoviesShow.vue";
// import MoviesEdit from "../views/MoviesEdit.vue";

// {
//   path: "/movies",
//   name: "Movies-index",
//   component: MoviesIndex
// },
// {
//   path: "/movies/new",
//   name: "Movies-new",
//   component: MoviesNew
// },
// {
//   path: "/movies/:id",
//   name: "Movies-show",
//   component: MoviesShow
// },
// {
//   path: "/movies/:id/edit",
//   name: "Movies-edit",
//   component: MoviesEdit
// }

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
