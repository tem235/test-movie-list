<template>
  <div class="movie-list">
    <h1>Movie List</h1>
    <div class="movie-list-search">
      <input class="movie-list-search__input" type="text">
      <button class="movie-list-search__button">Search</button>
    </div>
    <div class="movie-list-container">
      <MovieItem v-for="index in 10" :key="index"/>
    </div>

  </div>
</template>

<script>
import MovieItem from "@/components/MovieItem";

export default {
  name: "MovieList",
  components: {MovieItem}
}
</script>

<style scoped>
.movie-list {

}

.movie-list-container {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-gap: 30px;
  padding: 50px;
}

.movie-list-search {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 32px;

}

.movie-list-search__input {
  height: 100%;
  border-radius: 10px 0 0 10px;
  border: 2px solid #fe4141;
  background: transparent;
  color: #fff;
  padding-left: 10px;
  box-sizing: border-box;
}

.movie-list-search__input:focus {
  border: 2px solid #fe4151;
  outline: none;
}

.movie-list-search__button {
  height: 100%;
  width: 100px;
  border-radius: 0 10px 10px 0;
  border: 2px solid #fe4141;
  background: #fe4141;
  color: #fff;
  font-size: 20px;
}

.movie-list-search__button:hover {
  cursor: pointer;
  background: #a12828;
}
</style>