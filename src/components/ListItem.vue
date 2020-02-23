<template lang="html">
  <div id="container">
    <li>
      <h3>{{amiibo.gameSeries}}</h3>
        <h4>"{{amiibo.name}}"</h4>
        <img :src="amiibo.image">
        <br>
        <!-- <button>Add To Owned</button> -->
      </li>
  </div>

</template>

<script>
export default {
  name:"list-item",
  props:['amiibo']
}
</script>

<style lang="css" scoped>
img{
  height:160px;
  width:100px;
}

li{
  list-style: none;
}

#container{
  width:200px;
  border: 4pt double blue;
  border-radius: 25px;
  display: inline-block;
  margin:20px;
  text-align:center;

}
</style>
