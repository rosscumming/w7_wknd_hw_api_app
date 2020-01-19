<template>
  <select v-model='selectedFilm' @change='handleSelected'>
    <option v-for='film in films' :value='film'>{{film.title}}</option>
  </select>
</template>

<script>
import { eventBus } from '../main.js'


export default {


  name: 'selected-film',
  data(){
    return{
        selectedFilm: null
    }
  },
  props: ['films'],
  methods: {
    handleSelected(){
      eventBus.$emit('selected-film', this.selectedFilm);
    }
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
select {
margin: 0 auto;
display:flex;
}
</style>
