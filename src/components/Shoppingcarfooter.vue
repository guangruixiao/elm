<template>
    <div class="carfooter">
      <div class="content">
        <div class="left">
          <span class="logo-wrapper">
            <i class="icon-shopping_cart" ></i>
          </span>
          <span class="total">￥{{total}}</span>
          <span class="deliveryPrice">另需配送费{{deliveryPrice}}￥</span>
        </div>
        <div class="right">
          <span class="minPrice">￥{{minPrice}}起送 </span>
        </div>
      </div>
    </div>
</template>
<script>

export default {

  props: {
      deliveryPrice: {
      },
      minPrice: {
      }
  },
  data() {
    return {
      total: 0,
    };
  },

}
</script>
<style lang="scss" scoped>
  .carfooter{
    position:fixed;
    bottom:0;
    left:0;
    z-index:10;
    width:100%;
    height:50px;
    .content{
      display:flex;
      .left{
        flex:1;
      }
      .right{
        flex:0 0 105px;
        width:105px;
      }
    }
  }
</style>
