<template>
     <div class="sellerheader">
      <div class="main">
        <img class="sellerimg" v-bind:src=sellerMessage.avatar alt="">
        <div class="sellerinfo">
          <div class="name">{{sellerMessage.name}}</div>
          <div class="send">{{sellerMessage.description}}/{{sellerMessage.deliveryTime}}分钟送达</div>
          <div class="supports" v-if=sellerMessage.supports>
            <span>{{sellerMessage.supports[0].type}}</span>
            <span>{{sellerMessage.supports[0].description}}</span>
            <span>{{sellerMessage.supports.length}}</span>
          </div>
        </div>
      </div>
      <div class="bulletin">{{sellerMessage.bulletin}}</div>
     </div>
</template>
<script>
export default {
  props:["sellerMessage"]

}
</script>
<style>
</style>
