<template>
  <div class="movie-list">
    <h1>Movie List</h1>
    <div class="movie-list-search">
      <input class="movie-list-search__input" type="text">
      <button class="movie-list-search__button">Search</button>
    </div>
    <div class="movie-list-container">
      <MovieItem v-for="movie in movies"
                 :movie="movie"
                 :key="movie.id"
                 :admin="isAdmin"
      />
    </div>

  </div>
</template>

<script>
import MovieItem from "@/components/MovieItem";

export default {
  name: "MovieList",
  components: {MovieItem},
  data() {
    return {
      movies: [
        {
          id: 1,
          title: 'Interstellar',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/interstellar2_480x.progressive.jpg?v=1585846823',
          description: '',
          tags: [],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 2,
          title: 'Joker',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/de75d69d8743b0f549a2d0a32ce70ade_480x.progressive.jpg?v=1573572666',
          description: '',
          tags: [],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 3,
          title: 'Back to the future',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/0b2b67a1de6a06d1ce65e4ccc64047e3_a9f7318e-c5c4-4d2a-aed2-890bbfad883c_480x.progressive.jpg?v=1573590273',
          description: '',
          tags: [],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 4,
          title: 'Once upon a time in Hollywood',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/97f5d5fde1555eb38596f728a0fa0f92_139a11ca-a4e8-4aed-be97-03ba127ed518_480x.progressive.jpg?v=1573588887',
          description: '',
          tags: [],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 5,
          title: 'Quantum Of Solace',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/629ed1904353a7a3d0cc2b11d3c76b6e_d1eea8bc-f992-48db-90bf-1517e93c539b_480x.progressive.jpg?v=1573591629',
          description: '',
          tags: [],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 6,
          title: 'The Dark Knight',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/7463e8f00e8951717b3420d9a8615be7_dfb15650-b914-4ac6-83f4-b3ef42851cb3_480x.progressive.jpg?v=1573591354',
          description: '',
          tags: [],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 7,
          title: 'Spider-Man: Into the Spider-Verse',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/ba725a04a0416d8959f38334f6af0c33_2c5acc58-11b0-41ff-8220-37b69ae0e5e5_480x.progressive.jpg?v=1573588849',
          description: '',
          tags: [],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 8,
          title: 'La La Land',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/6294ae3e57013170bfffc9e8d77379c3_5c04d409-2a81-40e5-afd4-35556eeb6770_480x.progressive.jpg?v=1573593774',
          description: '',
          tags: [],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 9,
          title: 'Parasite',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/parasite_ver2_480x.progressive.jpg?v=1581347043',
          description: '',
          tags: [],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 10,
          title: 'Avengers: Endgame',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/108b520c55e3c9760f77a06110d6a73b_e97cf224-d57f-44e3-8477-4f5479cd746b_480x.progressive.jpg?v=1573616089',
          description: '',
          tags: [],
          rate: Math.floor(Math.random() * 5) + 1,
        },
      ],
      isAdmin: false,
    }
  }
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
  height: 40px;

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