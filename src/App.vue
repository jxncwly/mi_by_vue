<template>
  <div id="app">
    <top-bar></top-bar>
    <top-header></top-header>
    <top-banner></top-banner>
    <top-sub></top-sub>
    <goods></goods>
    <temp-footer></temp-footer>
    <play-video :play-config="playConfig"></play-video>
  </div>
</template>

<script>
import eventHub from './eventHub'
import TopBar from './components/TopBar'
import TopHeader from './components/TopHeader'
import TopBanner from './components/TopBanner'
import TopSub from './components/TopSub'
import Goods from './components/Goods'
import TempFooter from './components/TempFooter'
import PlayVideo from './components/PlayVideo'

export default {
  name: 'App',
  data () {
    return {
      playConfig: {}
    }
  },
  created () {
    this.recivePlayVideo()
  },
  beforeDestroy () {
    eventHub.$off('play')
    eventHub.$off('cancelPlay')
  },
  methods: {
    recivePlayVideo () {
      eventHub.$on('play', opts => {
        this.playConfig = opts
      })
      eventHub.$on('cancelPlay', opts => {
        this.playConfig = opts
      })
    }
  },
  components: {
    'top-bar': TopBar,
    'top-header': TopHeader,
    'top-banner': TopBanner,
    'top-sub': TopSub,
    'goods': Goods,
    'temp-footer': TempFooter,
    'play-video': PlayVideo
  }
}
</script>

<style>
@import './assets/css/base.css';
</style>
