<template>
  <div class="movie-item" :class="flip ? 'movie-item--flipped' : ''">
    <div class="movie-item-side movie-item-front ">
      <div class="movie-item-poster">

        <div class="movie-item-poster__filter-wrap">
          <img :src="movie.img" alt="">
        </div>

        <button class="movie-item-poster__button movie-item-poster__button--info" @click="flipCard">
          <img src="@/assets/info.svg" alt="">
        </button>

        <div v-if="admin" class="movie-item-poster-buttons">
          <button @click="$emit('edit', movie)" class="movie-item-poster__button">
            <img src="@/assets/pencil.svg" alt="">
          </button>
          <button @click="$emit('remove', movie.id)" class="movie-item-poster__button">
            <img src="@/assets/cancel.svg" alt="">
          </button>
        </div>

      </div>

      <div class="movie-item-content">
        <h3>{{ movie.title }}</h3>
        <div class="movie-item-content-rate">
          <img src="@/assets/star.svg" alt="">
          <b>{{ movie.rate }} / 5</b>
        </div>
      </div>
    </div>

    <div class="movie-item-side movie-item-back ">
      <button class="movie-item-poster__button movie-item-poster__button--info" @click="flipCard">
        <img src="@/assets/info.svg" alt="">
      </button>

      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias aliquam architecto dicta, dolore eaque eius
        error est eum in ipsam odit pariatur porro praesentium quae qui, recusandae, repudiandae temporibus tenetur.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieItem",
  props: ['movie', 'admin'],
  data() {
    return {
      flip: false,
    }
  },
  methods: {
    flipCard() {
      this.flip = !this.flip
    }
  }
}
</script>

<style lang="scss">
.movie-item {
  position: relative;
  max-width: 315px;
  min-width: 300px;
  height: 450px;
  box-shadow: 0 6px 18px rgba(0, 0, 0, .1);
  border-radius: 10px;
  transition: 300ms;
  color: #e7e7e7;
  overflow: visible;
  transform-style: preserve-3d;
  -webkit-transform-style: preserve-3d;
  font-family: 'Open Sans', sans-serif;

  &:hover {
    box-shadow: 1px 1px 25px 7px rgba(168, 59, 59, 0.3);


    .movie-item-poster__filter-wrap {
      filter: grayscale(0);
    }
  }

  &--flipped {
    transform: rotatey(-180deg);
  }

  &-side {
    position: absolute;
    z-index: 2;
    backface-visibility: hidden;
    overflow: auto;
    box-sizing: border-box;
  }

  &-front {
    border-radius: 10px;
    width: 100%;
  }

  &-back {
    height: 100%;
    padding: 20px;
    transform: rotatey(-180deg);
    border-radius: 10px;
  }

  &-poster {
    width: 100%;
    height: 370px;

    &__filter-wrap {
      width: 100%;
      height: 370px;
      filter: grayscale(0.5);
      transition: 300ms;

      img {
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }

    &-buttons {
      position: absolute;
      left: 10px;
      top: 10px;
      z-index: 2;
    }

    &__button {
      width: 40px;
      height: 40px;
      border: none;
      background: transparent;
      padding: 0;
      transition: 300ms;

      img {
        width: 30px;
        height: 30px;
      }

      &:hover {
        cursor: pointer;
        transform: scale(1.2);
      }

      &--info {
        position: absolute;
        top: 10px;
        right: 10px;

        img {
          width: 40px;
          height: 40px;
        }
      }
    }

  }

  &-content {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 15px;

    h3 {
      padding: 0;
      margin: 0;
      text-align: left;
      width: 80%;
      font-family: 'Montserrat', sans-serif;
      font-size: 20px;
    }

    &-rate {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 40px;
      width: 40px;
      border-radius: 50%;
      border: 2px solid #fe4141;
      padding: 5px;
      font-size: 12px;

      img {
        width: 18px;
        height: 18px;
        margin-bottom: 4px;
      }
    }
  }
}


</style>