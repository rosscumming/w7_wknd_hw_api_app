<template>
  <div id="app">
    <h1>Studio Ghibli Films</h1>
    <selected-film :films="films"></selected-film>
    <display-film :film="selectFilm"></display-film>
    <favourite-films :favouriteFilms='favouriteFilms'></favourite-films>
  </div>
</template>

<script>
import { eventBus } from './main.js'
import SelectFilm from './components/SelectFilm.vue'
import DisplayFilm from './components/DisplayFilm.vue'
import FavouriteFilms from './components/FavouriteFilms.vue'


export default {


  name: 'app',
  data(){
    return {
      'films': [],
      'favouriteFilms': [],
      'selectFilm': null
    };
  },
  mounted(){
    fetch('https://ghibliapi.herokuapp.com/films/')
    .then(response => response.json())
    .then(films => this.films = films)

    eventBus.$on('selected-film', filmObj => this.selectFilm = filmObj)
    eventBus.$on('send-favourite-film', filmObj => this.favouriteFilms.push(filmObj))
    eventBus.$on('delete-film-from-favourite', filmBeingDeletedId => {
      const filmObjectToDelete = this.films.find(film => film.id === filmBeingDeletedId);
      const index = this.favouriteFilms.indexOf(filmObjectToDelete);
      this.favouriteFilms.splice(index, 1)
    })

  },
  'components': {
    'selected-film': SelectFilm,
    'display-film': DisplayFilm,
    'favourite-films': FavouriteFilms
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
