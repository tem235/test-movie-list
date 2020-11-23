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

<style lang="scss">
@import url(https://fonts.googleapis.com/css?family=Montserrat:400,700);
@import url(https://fonts.googleapis.com/css?family=Open+Sans:400,300,600,700,800,300italic,400italic,600italic,700italic,800italic);

html {
  background: linear-gradient(
          rgba(30, 27, 38, 0.95),
          rgba(30, 27, 38, 0.95));
  min-height: 100vh;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-family: "Open Sans",sans-serif;
  margin: 0;
  padding: 0;
}
</style>
