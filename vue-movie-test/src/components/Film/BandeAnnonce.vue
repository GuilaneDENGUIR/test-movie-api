<template>
  <div id="bande-annonce">
    <iframe
      width="400"
      height="314"
      @click="toggleVideo"
      :src="linkTrailer"
    ></iframe>
    <div v-if="videoIsNotRunning">
      <img :src="imageURL" alt="Le Fondateur" />
      <h2>{{ titleMovie }}</h2>
      <p>{{ titleTrailer }}</p>
    </div>
  </div>
</template>

<script>
import env from "../../env.js";

export default {
  props: ["currentGenre"],
  data() {
    return {
      videoIsNotRunning: true,
      baseSecureURL: "https://image.tmdb.org/t/p/w185",
      imageURL: "",
      titleMovie: "",
      titleTrailer: "",
      linkTrailer: "https://www.youtube.com/embed/",
      id: "",
    };
  },
  methods: {
    toggleVideo() {
      this.videoIsNotRunning = !this.videoIsNotRunning;
    },
  },
  watch: {
    currentGenre() {
      fetch(
        `https://api.themoviedb.org/3/discover/movie?api_key=${env.apikey}&with_genres=${this.currentGenre}&sort_by=vote_average.desc&vote_count.gte=500`
      )
        .then((respond) => respond.json())
        .then((data) => {
          console.log(data);
          this.titleMovie = data.results[0].title;
          this.imageURL = this.baseSecureURL + data.results[0].poster_path;
          this.id = data.results[0].id;
          return fetch(
            `https://api.themoviedb.org/3/movie/${this.id}/videos?api_key=${env.apikey}`
          );
        })
        .then((response) => response.json())
        .then((data) => {
          // pas TOUS les films ont une vidéo
          console.log("VRAI", data);
          this.titleTrailer = data.results[0].name;
          this.linkTrailer =
            "https://www.youtube.com/embed/" + data.results[0].key;
          console.log(this.titleTrailer, this.linkTrailer);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style scoped>
#bande-annonce {
  position: relative;
  height: 35%;
  background-image: linear-gradient(rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.7));
}
iframe {
  position: absolute;
  bottom: 0;
  height: 100%;
  width: 100%;
}
img {
  width: 15%;
  position: absolute;
  bottom: 20px;
  left: 20px;
}
h2 {
  color: #fff;
  position: absolute;
  bottom: 15%;
  left: 22%;
}
p {
  color: #fff;
  position: absolute;
  bottom: 5%;
  left: 22%;
}

@media screen and (min-width: 1000px) {
  iframe {
    top: 0;
    right: 0;
    width: 100%;
    height: 100%;
  }

  #bande-annonce {
    height: 50%;
  }
  h2 {
    left: 20%;
  }
  p {
    left: 20%;
    bottom: 20px;
  }
}
</style>
