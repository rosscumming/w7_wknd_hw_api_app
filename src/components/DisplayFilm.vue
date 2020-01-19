<template>
  <div class="film-container" v-if="film">
    <i class="fas fa-film"></i>
    <h2>{{film.title}}</h2>
    <br />
    <h3>Description</h3>
    <p>{{film.description}}</p>
    <h3>Release Date</h3>
    <p>{{film.release_date}}</p>
    <h3>Director</h3>
    <p>{{film.director}}</p>
    <h3>Producer</h3>
    <p>{{film.producer}}</p>
    <div class="heart" @click="saveFavouriteFilm">
      <span>
        <i class="fas fa-heart"></i>
      </span>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "display-film",
  props: ["film"],
  methods: {
    saveFavouriteFilm() {
      eventBus.$emit("send-favourite-film", this.film);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.fa-film {
  margin: 10px 0 5px 0;
}

.heart,
.fa-heart {
  padding: 2px;
  border-radius: 5px;
  color: white;
  background: #ff5959;
  cursor: pointer;
}
h2,
h3 {
  text-transform: uppercase;
  font-weight: 100;
  letter-spacing: 2px;
  font-size: 1em;
  margin: 10px 0 5px 0;
  font-weight: bold;
}

h2 {
  border: 1px solid;
  border-radius: 5px;
  padding: 5px;
  color: white;
  background: #49beb7;
  margin-top: 0;
}

p {
  letter-spacing: 0.7px;
  font-size: 0.8em;
  padding: 0 10px 0 10px;
}

.film-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  height: 550px;
}
</style>
