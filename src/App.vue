<template>
  <div id="app">
    <seller ></seller>
    <menubar></menubar>
    <router-view ></router-view>
    <shoppingcar></shoppingcar>
  </div>
</template>

<script>
menubar
import seller from './components/seller'
import shoppingcar from './components/shoppingcar'
import menubar from './components/menubar'

export default {
  name: 'app',
  components: {
    seller,
    shoppingcar,
    menubar
  }
}
</script>

<style>


</style>
