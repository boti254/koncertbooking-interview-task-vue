<script>
import axios from "axios";

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
      const res = await axios.get(this.url)   
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
  <div class="pokecard_container">
      <div class="pokecard_outerflex">       
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
                    <span v-for="(ability) in this.firstFourOfList(abilities)" class="pokestat_abilities" >
                        {{ability.ability.name}}
                    </span>
                </div>
            </div>
          <img :src="this.imgUrl" class="pokeimg">
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
.pokecard_container{
    box-shadow: -0px 0px 0.5em rgb(227, 224, 224);
    border-radius: 5px;
    padding:30px;
    display: flex;
    flex-direction: row;
    margin-bottom: 25px;
}
.pokecard_outerflex{
  display: flex;
  flex-direction: row;
  padding-right: 200px;
  border-right: 2px solid rgb(238, 237, 237);
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
  color:rgb(100, 100, 100);
  font-weight: 500;
}
.pokestat_secondaryfont{
  color:rgb(130, 129, 129);
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
.pokeimg{
  max-height: 100%;
  max-width: 100%;
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
