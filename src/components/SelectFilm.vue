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
