<template>
  <div id="app">
    <h1>Studio Ghibli Films</h1>
    <selected-film :films="films"></selected-film>
    <display-film :film="selectFilm"></display-film>
  </div>
</template>

<script>
import { eventBus } from './main.js'
import SelectFilm from './components/SelectFilm.vue'
import DisplayFilm from './components/DisplayFilm.vue'

export default {


  name: 'app',
    data(){
      return {
        'films': [],
        'selectFilm': null
      };
    },
     mounted(){
       fetch('https://ghibliapi.herokuapp.com/films/')
        .then(response => response.json())
        .then(films => this.films = films)

        eventBus.$on('selected-film', filmObj => this.selectFilm = filmObj)
     },
     'components': {
      'selected-film': SelectFilm,
      'display-film': DisplayFilm
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
