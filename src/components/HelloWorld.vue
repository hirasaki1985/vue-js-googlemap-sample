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

    this.$map.addMarker({
      lat: -12.043330,
      lng: -77.028330,
      title: 'Lima',
      click: (e) => {
        console.log('click')
        if (this.$map.overlays.length === 0) {
          this.drawLabelInfo(this)
        } else {
          this.$map.removeOverlays()
        }
      }
    })
  },

  methods: {
    drawLabelInfo (el) {
      // let self = this

      this.$map.drawOverlay({
        lat: -12.043330,
        lng: -77.028330,
        layer: 'floatPane',
        verticalOffset: -170,
        content: '<div class="map-overlay">' +
        `<button id="map-overlay-close">close</button>` +
        `<div class="contents clearfix">コンテンツ</div>` +
        '</div></div>' +
        '</div>'
      })

      let overlayinterval = setInterval(() => {
        let overlayel = document.getElementById('map-overlay-close')
        console.log('setInterval()')
        console.log(overlayel)
        console.log(typeof (overlayel))
        if (typeof (overlayel) === 'object') {
          console.log('add event')
          overlayel.addEventListener('click', closeOverlay(), false)
          clearInterval(overlayinterval)
        }
        // clearInterval(overlayinterval)
      }, 1000)

      let closeOverlay = function () {
        return function () {
          el.$map.removeOverlays()
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
#map {
  width: 600px;
  height: 600px;
  margin:auto;
  padding:auto;
}

.map-overlay {
  border: 1px solid gray;
  background-color: white;
  border-radius: 10px;
  padding: 5px;
  width: 200px;
}

.field {
  padding: 5px 15px;
  border-bottom: 1px solid gray;

  &:last-child {
    border-bottom: none;
  }

  .label {
    color: darkgray;
  }

  .battery {
    float: right;
  }
}
</style>
