<template>
  <div class="film-container" v-if="film">
    <i class="fas fa-film"></i>
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

.fa-film{
  margin:10px 0 5px 0;
}
h2 {
text-transform: uppercase;
font-weight: 100;
letter-spacing: 2px;
font-size: 1em;
margin-top: 0;
}

.film-container{
  display:flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
</style>
