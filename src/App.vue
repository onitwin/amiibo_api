<template>
  <div id="app">
    <!-- <filter-controls/> -->
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
      filteredAmiibo: []
    }

  },
  mounted(){
    fetch('https://www.amiiboapi.com/api/amiibo/')//data now loading
    .then(res => res.json())
    .then (data => {
      this.allAmiibo=data;
      this.filteredAmiibo = data;
    })
  },
  components:{
    "list-all":ListAll,
    "filter-controls": FilterControls

  }
}
</script>

<style>

</style>
