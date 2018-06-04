<template>
  <div class="hello">
    <h1>map</h1>
    <div id="map"></div>
  </div>
</template>

<script>
import Vue from 'vue'
import GMaps from 'gmaps'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted () {
    const map = new GMaps({
      el: '#map',
      lat: -12.043333,
      lng: -77.028333
    })
    console.log(map)
    Vue.prototype.$map = map
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#map {
  width: 600px;
  height: 600px;
  margin:auto;
  padding:auto;
}
</style>
