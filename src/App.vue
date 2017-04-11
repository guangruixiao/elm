<template>
  <div id="app">
    <seller class="header" v-bind:sellerMessage="sellerinfo"></seller>
    <menubar class="tab border-1px" ></menubar>
    <router-view ></router-view>
    <shoppingcar></shoppingcar>
  </div>
</template>

<script>

import seller from './components/header/sellerheader'
import shoppingcar from './components/shoppingcarfooter'
import menubar from './components/menubar'

export default {
  name: 'app',
  data:function(){
        return {sellerinfo:{}}
    },
  mounted(){
      this.fetchdata();
    },
  methods:{
      fetchdata:function(){
        var self=this;
        this.$http.get('/api/seller')
         .then(function (response) {
            self.sellerinfo=response.data.data;
         })
         .catch(function (response) {
           console.log("没有接收到信息");
         });
      }
    },

  components: {
    seller,
    shoppingcar,
    menubar
  }
}
</script>

<style  lang="scss" scoped>

/* eslint-disable semi */
 @import './common/scss/_mixin';

 #app{
  .header{
    position:relative;
    width:100%;
    height:134px;
  }
  .tab {
    display:flex;
    width:100%;
    height:40px;
    line-height:40px;
    @include border-1px(rgba(7, 17, 27, 0.1))
  }
 }
</style>

