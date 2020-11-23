<template>
  <div class="modal">
    <div class="modal-inner">
      <button class="modal__close" @click="close">
        <img src="@/assets/cancel.svg" alt="">
      </button>
      <form v-if="create" class="modal-form">
        <input v-model="movie.title" type="text" placeholder="title create">
        <input v-model="movie.img" type="text" placeholder="image link">

        <textarea v-model="movie.description" placeholder="description"></textarea>
        <select v-model="movie.tags">
          <option disabled value="">Выберите один из вариантов</option>
          <option>action</option>
          <option>comedy</option>
          <option>drama</option>
          <option>adventure</option>
        </select>
        <input v-model.number="movie.rate" type="number" placeholder="rate">
        <button @click.prevent="$emit('create', movie)" type="submit">Submit</button>
      </form>

      <form v-else class="modal-form">
        <input v-model="editMovie.title" type="text" placeholder="title">
        <input v-model="editMovie.img" type="text" placeholder="image link">

        <textarea v-model="editMovie.description" placeholder="description"></textarea>
        <select v-model="editMovie.tags" multiple>
          <option disabled value="">Выберите один из вариантов</option>
          <option>action</option>
          <option>comedy</option>
          <option>drama</option>
          <option>adventure</option>
        </select>
        <input v-model.number="editMovie.rate" type="number" placeholder="rate">
        <button @click.prevent="update" type="submit">Submit</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: ['lastId', 'editMovie', 'create'],
  data() {
    return {
      movie: {
        id: this.lastId + 1,
        title: '',
        img: '',
        description: '',
        rate: '',
        tags: [],
      }
    }
  },
  methods: {
    update() {
      this.$emit('update', this.editMovie)
    },
    close() {
      this.movie = {
        id: this.lastId + 1,
        title: '',
        img: '',
        description: '',
        rate: '',
        tags: [],
      }
      this.$emit('close')
    }
  }


}
</script>

<style lang="scss">
.modal {
  display: grid;
  justify-content: center;
  align-items: center;
  position: fixed;
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.7);
  z-index: 10;

  &__close {
    position: absolute;
    top: 10px;
    right: 10px;
    width: 30px;
    height: 30px;
    border: none;
    background: transparent;

    &:hover {
      cursor: pointer;
    }
  }

  &-inner {
    position: relative;
    width: 400px;
    min-height: 300px;
    height: auto;
    background: #fff;
    padding: 40px;
    border-radius: 10px;
  }

  &-form {
    display: flex;
    flex-direction: column;

    input {
      margin-bottom: 10px;
      height: 30px;
    }

    textarea {
      margin-bottom: 10px;
      height: 100px;
    }

    select {
      margin-bottom: 10px;
    }
  }
}
</style>