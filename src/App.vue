<template>
  <div id="app">
    <top-bar></top-bar>
    <main-bar></main-bar>
    <main-bannner></main-bannner>
    <top-sub></top-sub>
  </div>
</template>

<script>
import TopBar from './components/TopBar'
import MainBar from './components/MainBar'
import MainBanner from './components/MainBanner'
import TopSub from './components/TopSub'
export default {
  components: {
    'top-bar': TopBar,
    'main-bar': MainBar,
    'main-bannner': MainBanner,
    'top-sub': TopSub
  }
}
</script>

<style>
@import './assets/css/base.css';
</style>
