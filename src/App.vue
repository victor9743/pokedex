<template>
  <div id="app">

    <div class="column is-half is-offset-one-quarter">

      <h4 class="is-size-4">Pokedex</h4>

          <input type="text" class="input is-rounded" placeholder="Buscar Pokemon pelo Nome" v-model="busca">
          <button class="button is-fullwidth is-success" id="busca_btn" @click="buscar">Busca</button>

          <div v-for="(poke, index) in filteredPokemons" :key="poke.url">

            <pokemon :num="index +1" :name="poke.name" :url="poke.url"/>
          </div>
    </div>
  


  </div>
</template>

<script>

import axios from 'axios';
import pokemon from './components/pokemon.vue';

export default {
  name: 'App',
  data(){
    return{
        pokemons: [],
        filteredPokemons:[],
        busca: ""
    }
    
  },
  created: function(){
    //  o codigo é executado quando a pagina carrega

    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(data =>{
      

      this.pokemons = data.data.results;
      this.filteredPokemons = data.data.results;

    })
  },
  components:{
    pokemon
  },

  methods: {

    buscar: function(){

      this.filteredPokemons = this.pokemons;

      if(this.busca == "" || this.busca == " "){
          this.filteredPokemons = this.pokemons

      }else{
          this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);

      }

    }

  },
  computed:{
    /*
    resultadoBusca: function(){
      if(this.busca == "" || this.busca == " "){
        return this.pokemons

      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }

    }
    */
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

#busca_btn{
  margin-top: 2%;
}
</style>
