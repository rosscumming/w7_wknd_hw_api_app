<template lang="html">
  <div class="footer" v-if='favouriteFilms.length'>
    <h1>Favourite Films</h1>
    <div class="favourite-films">
      <article class="fav-cont" v-for="film in favouriteFilms">
        <div class="item-cont">
        <h3>{{film.title}}</h3>
         <div class="foot-but" @click="removeFilmFromFavourites(film.id)">
          <i class="fas fa-trash-alt"></i>
         </div>
         </div>
      </article>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "favourite-films",
  props: ["favouriteFilms"],
  methods: {
    removeFilmFromFavourites(id) {
      eventBus.$emit("delete-film-from-favourite", id);
    }
  }
};
</script>

<style lang="css" scoped>
h1,
h3 {
  text-transform: uppercase;
  font-weight: 100;
  letter-spacing: 2px;
  font-size: 1.3em;
  margin: 20px 0 15px 0;
  font-weight: bold;
  padding-top: 15px;
  color: white;
}

h3 {
  letter-spacing: 0.7px;
  font-size: 0.8em;
  padding: 0 10px 0 10px;
  margin: 0 0 10px 0;
}

.footer {
  background: #352384;
  width: 100%;
  bottom: 0;
  padding-bottom: 30px;
  border-bottom-left-radius: 20px;
  border-bottom-right-radius: 20px;
}

.fa-trash-alt {
  padding: 2px;
  border-radius: 5px;
  color: white;
  cursor: pointer;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  width: 200px;
  bottom: 0;
  position: absolute;
}

.foot-but {
  background: #ff5959;
  width: 20px;
}

.item-cont {
  display: flex;
  justify-content: center;
  flex-direction: column;
  width: 200px;
  text-align: center;
  padding: 5px;
  bottom: 0;
  position: relative;
  margin: 0 auto;
  height: 75px;
}

.favourite-films {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  width: 600px;
}
</style>
