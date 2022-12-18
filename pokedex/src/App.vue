<template>
  <div id="app">
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',

  data(){
    return{
      pokemons : []
    }
    
  },

  created(){
    this.fetchPokemons();
  },

  methods:{
    fetchPokemons(){
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=150&offset=0").then(resp =>{
        this.pokemons = resp.data.results;
      }).catch(err=>console.log(err))

      
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
</style>
