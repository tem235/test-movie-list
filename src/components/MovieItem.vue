<template>
  <div class="movie-item">
    <div class="movie-item-front">
      <div class="movie-item-poster">
        <img src="https://via.placeholder.com/315x370" alt="">
        <button class="movie-item-poster__button movie-item-poster__button--info">
          <img src="@/assets/info.svg" alt="">
        </button>
        <div class="movie-item-poster-buttons">
          <button class="movie-item-poster__button">
            <img src="@/assets/pencil.svg" alt="">
          </button>
          <button class="movie-item-poster__button">
            <img src="@/assets/cancel.svg" alt="">
          </button>
        </div>
      </div>
      <div class="movie-item-content">
        <h3>Man of Steel</h3>
        <div class="movie-item-content-rate">
          <img src="@/assets/star.svg" alt="">
          <b>4.5 / 5</b>
        </div>
      </div>
    </div>

    <div class="movie-item-back">

    </div>
  </div>
</template>

<script>
export default {
  name: "MovieItem",
}
</script>

<style scoped>
.movie-item {
  max-width: 315px;
  height: 450px;
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0) 38%,
  rgba(255, 255, 255, 0.06) 39%, rgba(30, 27, 38, 0.88) 53%,
  rgba(30, 27, 38, 1) 55%);
  overflow: hidden;
  box-shadow: 0px 6px 18px rgba(0, 0, 0, .1);
  transition: 300ms;
  border-radius: 10px;
  color: #e7e7e7;
}

.movie-item:hover {
  transform: scale(1.03);
  box-shadow: 0px 10px 25px rgba(0, 0, 0, .08);
}

.movie-item-poster {
  position: relative;
  width: 100%;
  height: 370px;
}

.movie-item-poster img {
  width: 100%;
}


.movie-item-poster-buttons {
  position: absolute;
  left: 10px;
  top: 10px;
  z-index: 2;

}



.movie-item-poster__button {
  width: 40px;
  height: 40px;
  border: none;
  background: transparent;
  padding: 0;
  transition: 300ms;
}

.movie-item-poster__button img {
  width: 30px;
  height: 30px;
}

.movie-item-poster__button:hover {
  cursor: pointer;
  transform: scale(1.2);

}
.movie-item-poster__button--info {
  position: absolute;
  top: 10px;
  right: 10px;
}

.movie-item-poster__button--info img {
  width: 40px;
  height: 40px;
}

.movie-item-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 15px;

}

.movie-item-content-rate {
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
}

.movie-item-content-rate img {
  width: 18px;
  height: 18px;
  margin-bottom: 4px;
}
</style>