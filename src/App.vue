<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter" id="pokemonlogo">
      <figure class="image is-3by1">
        <img src="./assets/Pokemon-Logo.png">
      </figure>
      <hr>
        <img  width="350" height="350" src="./assets/pokedex.png">
      <div v-for="(poke, index) in pokemons" :key="index">
        <PokeInfo :name="poke.name" :url="poke.url" :num="index + 1"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import PokeInfo from './components/PokeInfo.vue';
export default {
  name: 'App',
  data(){
    return {
      pokemons: []
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
    })
  },
  components: {
    PokeInfo
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#pokemonlogo{
  margin-top: -5%;
}
</style>
