<template lang="html">
  <form>
    <label for="game-series">Game Series:</label>
    <select name="game-series">
      <option v-for="game in gameSeries">{{game.name}} </option>
    </select>
  </form>
</template>

<script>
export default {
  name:'filter-controls',
  data() {
    return {
      gameSeries: []
    }
  },
  mounted() {
    fetch('https://www.amiiboapi.com/api/gameseries/')
      .then(res => res.json())
      .then(data => this.gameSeries = data.amiibo)
  }
}
</script>

<style lang="css" scoped>
</style>
