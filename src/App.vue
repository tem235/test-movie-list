<template>
  <div id="app">
    <MovieList/>
  </div>
</template>

<script>


import MovieList from "@/components/MovieList";

export default {
  name: 'App',
  components: {MovieList},
}
</script>

<style>
html {
  background:linear-gradient(
      rgba(30,27,38, 0.95),
      rgba(30,27,38, 0.95));

  min-height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  margin: 0;
  padding: 0;
}
</style>
