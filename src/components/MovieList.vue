<template>
  <div class="movie-list">
    <h1>Movie List</h1>
    <form class="movie-list-search">
      <input v-model="query" class="movie-list-search__input" type="text">
      <button @click.prevent="search" type="submit" class="movie-list-search__button">Search</button>
    </form>
    <div class="movie-list-container">
      <MovieItem v-for="movie in moviesList"
                 :movie="movie"
                 :key="movie.id"
                 :admin="isAdmin"
                 @remove="removeItem"
                 @edit="editItem"
                 @sort="sortByTag"
      />
    </div>
    <button v-if="isAdmin" @click="addItem" class="movie-list__add">Add movie</button>
    <button @click="isAdmin = !isAdmin" class="movie-list__switch">Change role</button>
    <Modal v-show="showModal"
           :lastId="lastId"
           :editMovie="editMovie"
           :create="create"
           @create="createItem"
           @update="updateItem"
           @close="showModal = false"
    />
  </div>
</template>

<script>
import MovieItem from "@/components/MovieItem";
import Modal from "@/components/Modal";

export default {
  name: "MovieList",
  components: {Modal, MovieItem},
  data() {
    return {
      movies: [
        {
          id: 1,
          title: 'Interstellar',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/interstellar2_480x.progressive.jpg?v=1585846823',
          description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius\n' +
              '        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.',
          tags: ['adventure', 'action'],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 2,
          title: 'Joker',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/de75d69d8743b0f549a2d0a32ce70ade_480x.progressive.jpg?v=1573572666',
          description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius\n' +
              '        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.',
          tags: ['drama'],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 3,
          title: 'Back to the future',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/0b2b67a1de6a06d1ce65e4ccc64047e3_a9f7318e-c5c4-4d2a-aed2-890bbfad883c_480x.progressive.jpg?v=1573590273',
          description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius\n' +
              '        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.',
          tags: ['action', 'comedy', 'adventure'],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 4,
          title: 'Once upon a time in Hollywood',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/97f5d5fde1555eb38596f728a0fa0f92_139a11ca-a4e8-4aed-be97-03ba127ed518_480x.progressive.jpg?v=1573588887',
          description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius\n' +
              '        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.',
          tags: ['action', 'comedy', 'drama'],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 5,
          title: 'Quantum Of Solace',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/629ed1904353a7a3d0cc2b11d3c76b6e_d1eea8bc-f992-48db-90bf-1517e93c539b_480x.progressive.jpg?v=1573591629',
          description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius\n' +
              '        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.',
          tags: ['action', 'adventure'],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 6,
          title: 'The Dark Knight',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/7463e8f00e8951717b3420d9a8615be7_dfb15650-b914-4ac6-83f4-b3ef42851cb3_480x.progressive.jpg?v=1573591354',
          description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius\n' +
              '        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.',
          tags: ['action', 'adventure'],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 7,
          title: 'Spider-Man: Into the Spider-Verse',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/ba725a04a0416d8959f38334f6af0c33_2c5acc58-11b0-41ff-8220-37b69ae0e5e5_480x.progressive.jpg?v=1573588849',
          description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius\n' +
              '        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.',
          tags: ['action', 'comedy', 'adventure'],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 8,
          title: 'La La Land',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/6294ae3e57013170bfffc9e8d77379c3_5c04d409-2a81-40e5-afd4-35556eeb6770_480x.progressive.jpg?v=1573593774',
          description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius\n' +
              '        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.',
          tags: ['drama'],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 9,
          title: 'Parasite',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/parasite_ver2_480x.progressive.jpg?v=1581347043',
          description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius\n' +
              '        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.',
          tags: ['drama'],
          rate: Math.floor(Math.random() * 5) + 1,
        },
        {
          id: 10,
          title: 'Avengers: Endgame',
          img: 'https://cdn.shopify.com/s/files/1/0057/3728/3618/products/108b520c55e3c9760f77a06110d6a73b_e97cf224-d57f-44e3-8477-4f5479cd746b_480x.progressive.jpg?v=1573616089',
          description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius\n' +
              '        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.',
          tags: ['action', 'drama', 'adventure'],
          rate: Math.floor(Math.random() * 5) + 1,
        },
      ],
      moviesList: [],
      isAdmin: false,
      query: '',
      showModal: false,
      editMovie: {
        id: '',
        title: '',
        img: '',
        description: '',
        tags: [],
        rate: ''
      },
      create: true,
    }
  },
  created() {
    this.moviesList = this.movies
  },
  watch: {
    movies: function () {
      this.moviesList = this.movies
    }
  },
  computed: {
    lastId() {
      let lastItem = this.movies.length
      return this.movies[lastItem - 1].id
    }
  },
  methods: {
    addItem() {
      this.create = true
      this.showModal = !this.showModal;
    },
    createItem(movie) {
      this.movies.push(movie)
      this.showModal = false
    },
    editItem(movie) {
      this.create = false
      this.editMovie = Object.assign({}, movie)
      this.showModal = true
    },
    updateItem(movie) {
      if (confirm('Are you sure ?')) {
        let foundIndex = this.movies.findIndex(x => x.id === movie.id);
        this.$set(this.movies, foundIndex, movie)
        this.showModal = false
        this.editMovie = {
          id: '',
          title: '',
          img: '',
          description: '',
          tags: [],
          rate: ''
        }
      }
    },
    removeItem(id) {
      if (confirm('Are you sure ?')) {
        this.movies = this.movies.filter(movie => {
          return movie.id !== id
        })
      }
    },
    search() {
      if (this.query === '') {
        this.moviesList = [...this.movies]
      } else {
        this.moviesList = this.movies.filter(movie => {
          if (movie.title.toLowerCase().includes(this.query.toLowerCase())
              || movie.rate == this.query
              || movie.description.toLowerCase().includes(this.query.toLowerCase())
              || movie.tags.includes(this.query)) {
            return movie
          }

        })
      }
    },
    sortByTag(tag) {
      console.log(tag)
      this.moviesList = this.movies.filter(movie => {
        if (movie.tags.includes(tag)) {
          return movie
        }
      })
    },
  }
}
</script>

<style lang="scss">
.movie-list {

  h1 {
    font-family: 'Montserrat', sans-serif;
    color: #e7e7e7;

  }

  &-container {
    display: grid;
    //grid-template-columns: repeat(5, 1fr);
    grid-template-columns: repeat(auto-fit, minmax(315px, 1fr));
    grid-gap: 30px;
    padding: 50px;
    align-items: center;
    justify-items: center;
  }

  &-search {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 40px;

    &__input {
      height: 100%;
      border-radius: 10px 0 0 10px;
      border: 2px solid #fe4141;
      background: transparent;
      color: #fff;
      padding-left: 10px;
      box-sizing: border-box;

      &:focus {
        border: 2px solid #fe4151;
        outline: none;
      }
    }

    &__button {
      height: 100%;
      width: 100px;
      border-radius: 0 10px 10px 0;
      border: 2px solid #fe4141;
      background: #fe4141;
      color: #fff;
      font-size: 20px;

      &:hover {
        cursor: pointer;
        background: #a12828;
      }
    }
  }

  &__switch {
    position: fixed;
    bottom: 10px;
    right: 10px;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    border: none;
    background: #fe4141;
    color: #fff;
    font-family: 'Open Sans', serif;
    font-size: 14px;

    &:hover {
      cursor: pointer;
      background: #a12828;
    }

  }

  &__add {
    position: fixed;
    bottom: 100px;
    right: 10px;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    border: none;
    background: #fe4141;
    color: #fff;
    font-family: 'Open Sans', serif;
    font-size: 14px;

    &:hover {
      cursor: pointer;
      background: #a12828;
    }

  }
}

</style>