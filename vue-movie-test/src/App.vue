<template>
  <the-header></the-header>
  <main>
    <bande-annonce
      :currentGenre="currentGenre"
      class="container"
    ></bande-annonce>
    <display-film v-on:changeGenre="uptadeGenre($event)"></display-film>
  </main>
</template>

<script>
import BandeAnnonce from "./components/Film/BandeAnnonce.vue";
import TheHeader from "./components/TheHeader.vue";
import DisplayFilm from "./components/Film/DisplayFilm.vue";

export default {
  name: "App",
  components: {
    BandeAnnonce,
    TheHeader,
    DisplayFilm,
  },
  data() {
    return {
      currentGenre: "",
    };
  },
  methods: {
    uptadeGenre(uptadedGenre) {
      this.currentGenre = uptadedGenre;
      this.$emit("changeGenre", uptadedGenre);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}
body,
#app {
  height: 100vh;
}
main {
  height: 100%;
}

.container {
  height: 30%;
}

@media screen and (min-width: 1000px) {
  body,
  #app {
    width: 90%;
    margin: auto;
  }
}
</style>
