<template lang="html">
  <form v-on:submit.prevent>
    <label for="game-series">Game Series:</label>
    <select v-on:change="handleSelect" name="game-series" v-model="selectedGame">
      <option v-for="game in gameSeries" :value="game">{{game.name}} </option>
    </select>
  </form>
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name:'filter-controls',
  data() {
    return {
      gameSeries: [],
      selectedGame:{}
    }
  },
  mounted() {
    fetch('https://www.amiiboapi.com/api/gameseries/')
      .then(res => res.json())
      .then(data => this.gameSeries = data.amiibo)
  },
  methods:{
    handleSelect(){
      eventBus.$emit('game-selected',this.selectedGame)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
