<template>
  <div class="list-genre">
    <form @submit.prevent="">
      <div>
        <input
          type="radio"
          id="comedie"
          name="genre"
          value="35"
          v-model="checkedBox"
          @click="changeGenre"
        />
        <label for="comedie">Comedie</label>
      </div>
      <div>
        <input
          type="radio"
          id="aventure"
          name="genre"
          value="12"
          v-model="checkedBox"
          @click="changeGenre"
        />
        <label for="aventure">Aventure</label>
      </div>
      <div>
        <input
          type="radio"
          id="fantastique"
          name="genre"
          value="14"
          v-model="checkedBox"
          @click="changeGenre"
        />
        <label for="fantastique">Fantastique</label>
      </div>
      <div>
        <input
          type="radio"
          id="animation"
          name="genre"
          value="16"
          v-model="checkedBox"
          @click="changeGenre"
        />
        <label for="animation">Animation</label>
      </div>
      <div>
        <input
          type="radio"
          id="action"
          name="genre"
          value="28"
          v-model="checkedBox"
          @click="changeGenre"
        />
        <label for="action">Action</label>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      checkedBox: "",
    };
  },
  methods: {
    changeGenre() {
      // checkedBox renvoie la valeur avant changement, le v-model n'est pas dinamique ?
      this.$emit("changeGenre", this.checkedBox);
    },
  },
};
</script>
<style scoped>
.list-genre {
  width: 40%;
  height: 250px;
  border: 1px solid black;
  margin: 30px 10px;
}

.list-genre div {
  margin: 20px 10px;
}

@media screen and (min-width: 1000px) {
  .list-genre {
    height: 300px;
  }
  .list-genre div {
    margin: 30px 10%;
  }
  input {
    margin-right: 10px;
  }
}
</style>
