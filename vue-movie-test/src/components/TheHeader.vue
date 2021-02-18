<template>
  <header>
    <a href="www.google.com"> A propos de We Movies</a>
    <form @submit.prevent="searchMovie">
      <input type="text" v-model="movieSearched" />
    </form>
  </header>
</template>

<script>
import env from "../env.js";

export default {
  data() {
    return {
      movieSearched: "",
    };
  },
  methods: {
    searchMovie() {
      fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=${env.apikey}&query=${this.movieSearched}`
      )
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          //autocompletion WIP
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style scoped>
header {
  height: 8%;
  display: flex;
  align-content: center;
  justify-content: space-between;
  padding: 10px 16px;
  margin-top: 10px;
  font-size: 1.1em;
}

a {
  color: black;
}

header input {
  height: 1.4rem;
  width: 180px;
}

@media screen and (min-width: 1000px) {
  header {
    margin: auto;
    align-items: center;
    height: 10%;
  }
}
</style>
