<script>
import PokemonStats from "./PokemonStats.vue";

export default{
    name:'PokemonCard',
    props:{
        name: String,
        url: String,
        index: Number
    },
    methods:{
      remove(){
        this.$parent.remove(this.index)
      },
    },
    components:{
      PokemonStats
    }
}
</script>

<template>
  <div class="pokecard_container">
    <div class="pokecard_outerflex">
      <PokemonStats :name="this.name" :url="this.url"/>
    </div>
    <div class="pokedesc_container">
      <p class="pokestat_secondaryfont pokedesc">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut vestibulum ut nibh a tempus. Duis ullamcorper diam eu nunc mollis tempus. Sed venenatis dapibus dictum. Curabitur varius justo non auctor congue. Praesent aliquet odio non posuere faucibus. Nunc quis ultricies ex. Vivamus lacus lacus, viverra nec aliquet eu, luctus quis tellus. Integer in fringilla nisi, vitae vulputate eros. In malesuada tellus id ex posuere, sit amet elementum ante facilisis. Phasellus ornare et ante quis ullamcorper.
      </p>
      <button class="pokebutton_delete" @click="remove()">
        Törlés
      </button>
    </div>
  </div>       
</template>

<style lang="scss">
$shadow-color: rgb(227, 224, 224);

@media screen and (max-width: 1450px) { 
    .pokedesc { 
        display: none;
    }
}
.pokecard_container{
    box-shadow: -0px 0px 0.5em $shadow-color;
    border-radius: 5px;
    padding:30px;
    display: flex;
    flex-direction: row;
    margin-bottom: 25px;
}
.pokecard_outerflex{
  display: flex;
  flex-direction: row;
  padding-right: 50px;
  border-right: 2px solid $shadow-color;
}
.pokedesc_container{
  display: flex;
  flex-direction: column;
  margin-left: 50px;
  margin-right: 50px;
}
.pokedesc{
  padding-bottom: 50px;
}
.pokebutton_delete{
  background-color: #b0224f;
  border: none;
  color: white;
  padding: 10px 32px;
  text-align: center;
  text-decoration: none;
  font-size: 16px;
  margin: 0 100px;
  border-radius: 5px;
}
</style>
