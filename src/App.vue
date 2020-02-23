<template>
  <div id="app">
    <h1 id="greeting">Itsa Me, Mario!!</h1>
    <filter-controls id="filt"/>
    <img  id="reset" src="./assets/questionBlock.png" v-on:click="reset">
    <audio id="myAudio">
      <source src="./assets/smw_coin.wav" type="audio/ogg">
  </audio>

    <list-all :allAmiibo="filteredAmiibo"></list-all>
  </div>
</template>

<script>
import ListAll from './components/ListAll.vue';
import FilterControls from './components/FilterControls.vue'
import {eventBus} from './main.js';
import Block from './components/Block'
export default {
  name: 'App',
  data(){
    return{
      allAmiibo:[],
      chosenAmiibo:null,
      selectedGame:null,
      filteredAmiibo:[],
      image:"./assets/questionBlock.png",
      sound:"./assets/smw_coin.wav"
    }

  },
  mounted(){
    fetch('https://www.amiiboapi.com/api/amiibo/')//data now loading
    .then(res => res.json())
    .then (data => {
      this.allAmiibo=data.amiibo;
      this.filteredAmiibo = data.amiibo;

      eventBus.$on('game-selected',(game)=>{
        this.selectedGame=game
      })
    })
  },
  components:{
    "list-all":ListAll,
    "filter-controls": FilterControls,
    "block":Block

  },
  computed:{
    filters:function(){
      return this.filteredAmiibo = this.filteredAmiibo.filter(amiibo => amiibo.gameSeries === this.selectedGame.name)}


  },
  methods:{
     reset:function(){
       var myBlock = document.getElementById("myAudio");
       myBlock.play()
       this.selectedGame=null
       this.filteredAmiibo=this.allAmiibo;

    }

  }



}
</script>

<style>


@@font-face {
  font-family:"Mario";
  src:url(./assets/SuperMario256.ttf);
}


#reset{
  height:100px;
  width:100px;
  display: inline-flex;
  margin-left: 400px;
}

#reset:active{
  transform: translatey(4px);
}

#filt{
  display: inline-flex;
}
</style>
