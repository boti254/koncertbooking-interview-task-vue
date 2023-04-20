<script>
import axios from "axios";
import PokemonCard from "./PokemonCard.vue"

export default{
  methods:{
      remove(index){
        this.pokemons.splice(index,1)
      }
  },
  components:{
    PokemonCard
  },
  data(){
    return{
      pokemons: [],
    }
  },
  async created(){
    try{
      const pokemonLimit = '10'
      const pokemonOffset = '0'
      const url = `https://pokeapi.co/api/v2/pokemon?offset=${pokemonOffset}&limit=${pokemonLimit}`

      await axios.get(url)   
      .then(response => {
        this.pokemons = response.data.results
      })
    }catch(err){
      console.log(err)
    }
  }
}
</script>

<template>
  <div class="pokelist_container">
    <ul style="list-style-type: none;">
      <li v-for="(pokemon,index) in pokemons" :key="pokemon.name">
        <PokemonCard :name="pokemon.name" :index="index" :url="pokemon.url"/>
      </li>
    </ul>
  </div>
</template>

<style lang="scss">
$shadow-color: rgb(200, 200, 200);

.pokelist_container{
    box-shadow: -2px 2px 0.3em $shadow-color;
    border-radius: 5px;
    padding:30px;
}
</style>
