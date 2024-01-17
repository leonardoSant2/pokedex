<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter" id="pokemonlogo">
      <figure class="image is-3by1">
        <img src="./assets/Pokemon-Logo.png">
      </figure>
      <hr>
        <img  width="350" height="350" src="./assets/pokedex.png">
        <input type="text" placeholder="Buscar pokemon pelo nome" v-model="busca" class="input is-rounded">
        <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar">Buscar</button>
        <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
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
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components: {
    PokeInfo
  },
  methods:{
      buscar: function(){
        if(this.busca == '' || this.busca == ' '){
          this.filteredPokemons = this.pokemons;
        }else{
          this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name.toLowerCase().includes(this.busca.toLowerCase()));
        }
      }
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
