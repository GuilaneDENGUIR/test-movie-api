<template>
  <div class="container">
    <list-genre v-on:changeGenre="uptadeGenre($event)"></list-genre>
    <list-film :genre="currentGenre"></list-film>
  </div>
</template>

<script>
import ListGenre from "./ListGenre.vue";
import ListFilm from "./ListFilm.vue";

export default {
  components: {
    ListGenre,
    ListFilm,
  },
  data() {
    return {
      currentGenre: "",
    };
  },
  methods: {
    //décalage du Genre car v-model non dinamique ?
    uptadeGenre(uptadedGenre) {
      this.currentGenre = uptadedGenre;
      this.$emit("changeGenre", uptadedGenre);
    },
  },
};
</script>

<style scoped>
.container {
  width: 100%;
  display: flex;
  flex-direction: row;
}
</style>
