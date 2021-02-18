<template>
  <div class="column">
    <base-card v-for="movie in results" :key="movie.id" class=" main">
      <img
        :src="'https://image.tmdb.org/t/p/w185' + movie.poster_path"
        alt="Poster du film"
      />
      <div class="details">
        <div class="title">
          <h2>{{ movie.title }}</h2>
          <div class="container">
            <p>{{ movie.vote_average }}</p>
            <p>({{ movie.vote_count }})</p>
          </div>
        </div>
        <p>
          <strong>{{ movie.release_date }}</strong>
        </p>
        <p class="movie-overview">{{ movie.overview }}</p>
        <base-button @click="triggerModal($event, movie.id)" id="btn_details">
          Plus de détails
        </base-button>
      </div>
    </base-card>
  </div>
  <teleport to="body">
    <modal-movie
      v-if="modalIsActive"
      :id_movie="id_movie"
      v-on:closeModal="closeModal($event)"
    ></modal-movie>
  </teleport>
</template>

<script>
import env from "../../env.js";
import ModalMovie from "./ModalMovie.vue";

export default {
  props: ["genre"],

  components: {
    ModalMovie,
  },

  data() {
    return {
      results: [],
      id_movie: "",
      modalIsActive: false,
    };
  },
  methods: {
    triggerModal(event, id_movie) {
      this.id_movie = id_movie;
      this.modalIsActive = true;
    },
    closeModal(isActive) {
      this.modalIsActive = isActive;
    },
  },
  watch: {
    genre() {
      fetch(
        `https://api.themoviedb.org/3/discover/movie?api_key=${env.apikey}&with_genres=${this.genre}`
      )
        .then((response) => response.json())
        .then((data) => {
          this.results = data.results;
          console.log(this.results);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style scoped>
.column {
  display: flex;
  flex-direction: column;
  width: 50%;
}

.container {
  display: flex;
  flex-direction: row;
}
.main {
  display: flex;
  flex-direction: column;
  position: relative;
}

.title {
  display: flex;
  flex-direction: column;
}

img {
  width: 40%;
  margin: 10px auto;
}
h2 {
  margin-left: 5px;
  margin-top: 5px;
  font-size: 1em;
}
p {
  margin: 5px;
}

#btn_details {
  position: absolute;
  bottom: 1%;
  right: 1%;
}
.movie-overview {
  height: 40%;
  overflow: auto;
}
@media screen and (min-width: 1000px) {
  .movie-overview {
    height: 30%;
    overflow: auto;
  }

  .title {
    flex-direction: row;
  }
  .main {
    flex-direction: row;
  }
  img {
    display: block;
    height: 90%;
    width: 25%;
    margin: auto;
  }
}
</style>
