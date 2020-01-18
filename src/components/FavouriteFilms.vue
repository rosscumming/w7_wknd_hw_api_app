<template lang="html">
  <div v-if='favouriteFilms.length'>
    <h1>Favourite Films</h1>
    <div class="favourite-films">
      <article v-for="film in favouriteFilms">
        <h3>{{film.title}}</h3>
        <button type="button" @click="removeFilmFromFavourites(film.id)">Unfavourite me</button>
      </article>
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'favourite-films',
  props: ['favouriteFilms'],
  methods: {
    removeFilmFromFavourites(id){
      eventBus.$emit('delete-film-from-favourite', id)
    }
  }
}
</script>

<style lang="css" scoped>

</style>
