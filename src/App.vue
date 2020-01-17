<template>
  <div id="app">
    <h1>Studio Ghibli Films</h1>
    <selected-film :films="films"></selected-film>
  </div>
</template>

<script>

import SelectFilm from './components/SelectFilm'

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
     },
     'components': {
      'selected-film': SelectFilm
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
