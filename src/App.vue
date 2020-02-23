<template>
  <div id="app">
    <filter-controls/>
    <list-all :allAmiibo="filteredAmiibo"></list-all>
  </div>
</template>

<script>
import ListAll from './components/ListAll.vue';
import FilterControls from './components/FilterControls.vue'
import {eventBus} from './main.js';

export default {
  name: 'App',
  data(){
    return{
      allAmiibo:[],
      chosenAmiibo:null,
      selectedGame:null,
      filteredAmiibo:[]
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
    "filter-controls": FilterControls

  },
  computed:{
    filters:function(){
      return this.filteredAmiibo = this.filteredAmiibo.filter(amiibo => amiibo.gameSeries === this.selectedGame.name)}


  }



}
</script>

<style>
</style>
