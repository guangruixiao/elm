<template>
  <div id="app">
    <seller ></seller>
    <menubar class="tab" ></menubar>
    <router-view ></router-view>
    <shoppingcar></shoppingcar>
  </div>
</template>

<script>
menubar
import seller from './components/sellerheader'
import shoppingcar from './components/shoppingcarfooter'
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

<style  lang="scss" scoped>
 #app{
  .tab {
    display:flex;
    width:100;
    height:40px;
    line-height:40px;
  }
 }

</style>

