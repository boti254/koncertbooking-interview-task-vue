<script>
import axios from "axios";

export default{
    name:'PokemonStats',
    props:{
        name: String,
        url: String,
    },
    methods:{
      capitalizeFirst(str){
        return str.charAt(0).toUpperCase() + str.slice(1)
      },
      firstFourOfList(list){
        if(list.length>4){
          return list.slice(0,4)
        }else{
          return list
        }
      }
    },
    data(){
        return{
            height: Number,
            weight: Number,
            hp: Number,
            attack: Number,
            defense: Number,
            stats: [],
            abilities: [],
            imgUrl: String,
        }
    },
    async created(){
    try{
      await axios.get(this.url)   
      .then(response => {
        this.height = response.data.height
        this.weight = response.data.weight
        this.stats = response.data.stats
        this.hp = this.stats[0].base_stat
        this.attack = this.stats[1].base_stat
        this.defense = this.stats[2].base_stat
        this.abilities = response.data.abilities
        this.imgUrl = response.data.sprites.front_default
      })
    }catch(err){
      console.log(err)
    }
  },
}
</script>

<template>
  <div class="pokestat_container">
    <h1 class="pokestat_paddingbottom">{{capitalizeFirst(this.name)}}</h1>
    <div class="pokestat_paddingbottom pokestat_hw">
      <span class="pokestat_primaryfont">Magasság / Súly : {{ this.height }} / {{ this.weight }}</span>
    </div>
    <h4 class="pokestat_paddingbottom pokestat_secondaryfont">HP : {{ this.hp }}</h4>
    <h4 class="pokestat_paddingbottom pokestat_secondaryfont">Sebzés : {{ this.attack }}</h4> 
    <h4 class="pokestat_paddingbottom pokestat_secondaryfont">Védelem : {{ this.defense }}</h4>   
    <div class="pokestat_abilitycontainer pokestat_secondaryfont">
      <span>Képességek :</span>
      <span v-for="(ability) in this.firstFourOfList(abilities)" :key="ability.ability.name" class="pokestat_abilities" >
         {{ability.ability.name}}
      </span>
    </div>
  </div>
  <div class="pokeimg_container">
    <img :src="this.imgUrl" class="pokeimg">
  </div>
</template>

<style lang="scss">
$primary-font-color: rgb(100, 100, 100);
$secondary-font-color: rgb(130, 129, 129);

@media screen and (max-width: 1450px) { 
    .pokeimg { 
        display: none;
    }
}
.pokeimg{
  max-height: 100%;
  max-width: auto;
}
.pokeimg_container{
  display: flex;
  height: auto;
  width: 200px;
  justify-content: center;
  align-items: center;
}
.pokestat_container{
  display: flex;
  flex-direction: column;
  min-width: 350px;
  justify-content: center;
}
.pokestat_paddingbottom{
  padding-bottom: 10px;
}
.pokestat_hw{
  display: flex;
  flex-direction: row;
  align-items: baseline;;
}
.pokestat_primaryfont{
  color: $primary-font-color;
  font-weight: 500;
}
.pokestat_secondaryfont{
  color: $secondary-font-color;
  font-weight: 100;
  font-size: small;
}
.pokestat_abilitycontainer{
  display: flex;
  flex-direction: row;
}
.pokestat_abilities{
  padding-right: 20px;
  padding-left:10px
}

</style>
