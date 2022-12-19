<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      POKEDEX<br>
      <input class="input is-rounded" type="text" placeholder="buscar pokemon pelo nome" v-model="pokemonSearch">
      <button id="btn-search" class="button is-medium is-responsive is-primary is-rounded" @click="findPokemon">Buscar</button>
      <div class="poke" v-for="(pokemon, index) in filteredPokemons" :key="pokemon.url">
      <Pokemon :name = "pokemon.name" :url= "pokemon.url" :num ="index+1" />
    </div>
    </div>
    
  </div>
</template>

<script>

import axios from 'axios';
import Pokemon from './components/Poke-Mon.vue';

export default {
  name: 'App',

  components:{
    Pokemon
  },


  data(){
    return{
      pokemons : [],
      pokemonSearch:'',
      filteredPokemons:[]
    }
    
  },

  created(){
    this.fetchPokemons();
  },

  methods:{
    fetchPokemons(){
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=150&offset=0").then(resp =>{
        this.pokemons = resp.data.results;
        this.filteredPokemons = resp.data.results;
      }).catch(err=>console.log(err))
    },

    findPokemon(){
      let busca = this.pokemonSearch.toLowerCase();
      if(this.pokemonSearch === '' || this.pokemonSearch === ' '){
        return this.filteredPokemons = this.pokemons;
      }
      return this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name === busca);
    }

  },

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
.poke{
  margin-top:2%;
}

#btn-search{
  margin-top:2%;
  width:100%;
}
</style>
