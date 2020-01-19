<template>
  <div id="app">
    <div id="container">
      <h1>Studio Ghibli Films</h1>
      <selected-film :films="films"></selected-film>
      <display-film :film="selectFilm"></display-film>
      <favourite-films :favouriteFilms="favouriteFilms"></favourite-films>
    </div>
  </div>
</template>

<script>
import { eventBus } from "./main.js";
import SelectFilm from "./components/SelectFilm.vue";
import DisplayFilm from "./components/DisplayFilm.vue";
import FavouriteFilms from "./components/FavouriteFilms.vue";

export default {
  name: "app",
  data() {
    return {
      films: [],
      favouriteFilms: [],
      selectFilm: null
    };
  },
  mounted() {
    fetch("https://ghibliapi.herokuapp.com/films/")
      .then(response => response.json())
      .then(films => (this.films = films));

    eventBus.$on("selected-film", filmObj => (this.selectFilm = filmObj));
    eventBus.$on("send-favourite-film", filmObj =>
      this.favouriteFilms.push(filmObj)
    );
    eventBus.$on("delete-film-from-favourite", filmBeingDeletedId => {
      const filmObjectToDelete = this.films.find(
        film => film.id === filmBeingDeletedId
      );
      const index = this.favouriteFilms.indexOf(filmObjectToDelete);
      this.favouriteFilms.splice(index, 1);
    });
  },
  components: {
    "selected-film": SelectFilm,
    "display-film": DisplayFilm,
    "favourite-films": FavouriteFilms
  }
  //
  //  computed: {
  //  selectedFilmObj(){
  //    return this.films.find(film => film.id === this.selectFilm)
  //  }
  // }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Lato:400,700");
html {
  min-height: 100%;
}

body {
  background: linear-gradient(
    to top,
    #ff5959 0%,
    #ff5959 50%,
    #facf5a 50%,
    #facf5a 100%
  );
}

#container {
  position: relative;
  margin: 30px 0 0 0;
  background: #f9f9fa;
  width: 600px;
  min-height: 700px;
  border-radius: 20px;
 box-shadow: 5px 5px 20px rgba(17, 17, 31, 0.3);
}

#app {
  display: flex;
  justify-content: center;
  font-family: "Lato", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

h1 {
  text-align: center;
  font-weight: 200;
}
</style>
