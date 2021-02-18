<template>
  <div class="modal">
    <div class="modal_content">
      <button @click="closeModal">X</button>
      <iframe :src="linkTrailer" frameborder="0"></iframe>
      <div class="title">
        <h2>{{ titleTrailer }}</h2>
        <p>Bande annonce EN</p>
      </div>
      <div class="note">
        <p>Film : {{ titleMovie }}</p>
        <p>
          <span>{{ voteAverage }}</span> pour {{ voteCount }} utilisateurs
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import env from "../../env.js";

export default {
  props: ["id_movie"],
  data() {
    return {
      titleMovie: "",
      titleTrailer: "",
      voteCount: "",
      voteAverage: "",
      linkTrailer: "https://www.youtube.com/embed/",
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal", false);
    },
  },
  beforeMount() {
    fetch(
      `https://api.themoviedb.org/3/movie/${this.id_movie}?api_key=${env.apikey}&append_to_response=videos`
    )
      .then((response) => response.json())
      .then((data) => {
        this.titleTrailer = data.videos.results[0].name;
        this.voteCount = data.vote_count;
        this.voteAverage = data.vote_average;
        this.linkTrailer =
          this.linkTrailer + data.videos.results[0].key + "?&controls=0";
        this.titleMovie = data.title;
        console.log(data);
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  display: flex;
  align-items: center;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
}

.modal_content {
  position: relative;
  width: 90%;
  height: 80%;
  display: block;
  background: #fff;
  margin: auto;
}

.title {
  display: flex;
  flex-direction: row;
  margin: 0 5%;
}

button {
  border-radius: 50%;
  padding: 5px;
  position: absolute;
  top: -13px;
  right: -13px;
}

iframe {
  display: block;
  width: 90%;
  height: 40%;
  margin: 5% auto;
}

h2,
.title p {
  font-size: 1em;
  margin: 5px 5px 5px 0;
}

span {
  color: gold;
  background: #000;
  padding: 2px;
  border-radius: 3px;
}

.note {
  display: flex;
  flex-direction: row;
  margin: 0 5%;
}

.note p:first-child {
  margin-right: 3px;
}

@media screen and (min-width: 1000px) {
  iframe {
    width: 60%;
    height: 70%;
    margin-bottom: 1%;
  }
  .note,
  .title {
    margin: 0 20%;
  }
}
</style>
