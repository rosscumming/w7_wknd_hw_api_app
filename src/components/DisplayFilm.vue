<template>
  <div v-if="film">
      <h2>{{film.title}}</h2><br>
      <h3> Description:</h3>
      <p>{{film.description}}</p>
      <h3>Release Date:</h3>
      <p>{{film.release_date}}</p>
      <h3>Director:</h3>
      <p>{{film.director}}</p>
      <h3>Producer:</h3>
      <p>{{film.producer}}</p>
      <button @click="saveFavouriteFilm">Favourite This Film</button>

  </div>




</template>

<script>
import { eventBus } from '../main.js'


export default {
  name: 'display-film',
  props: ['film'],
  methods: {
    saveFavouriteFilm(){
      eventBus.$emit('send-favourite-film', this.film);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
