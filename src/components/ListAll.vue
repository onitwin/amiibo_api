<template lang="html">
<div>
  <ul>
    <list-item v-for="(amiibo, index) in allAmiibo" :amiibo="amiibo" :key="index"></list-item>
  </ul>
  </div>

</template>

<script>
import ListItem from './ListItem.vue'
export default {
  name:'list-all',
  props:["allAmiibo"],
  components:{
    "list-item":ListItem
  }
}
</script>

<style lang="css" scoped>
</style>
