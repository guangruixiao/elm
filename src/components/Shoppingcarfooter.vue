<template>
    <div class="carfooter">
      <div class="content">
        <div class="left">
          <span class="logo-wrapper">
            <i class="icon-shopping_cart" ></i>
          </span>
          <span class="total">￥{{total}}</span>
          <span class="desc">另需配送费{{deliveryPrice}}￥</span>
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
    color: rgba(255, 255, 255, 0.4);
    .content{
      display:flex;
      background: #141d27;
      .left{
        flex:1;
        .logo-wrapper{
          display: inline-block;
          vertical-align: top;
          position: relative;
          top: -10px;
          margin: 0 12px;
          padding: 6px;
          width: 56px;
          height: 56px;
          box-sizing: border-box;
          border-radius: 50%;
          background: #141d27;
          text-align: center;
          .icon-shopping_cart{
            line-height: 44px;
            font-size: 24px;
            color: #80858a;
          }
        }
        .total{
          display: inline-block;
          margin-top: 12px;
          line-height: 24px;
          padding-right: 12px;
          box-sizing: border-box;
          border-right: 1px solid rgba(255, 255, 255, 0.1);
          font-size: 16px;
          font-weight: 700;
        }
        .desc{
          display: inline-block;
          vertical-align: top;
          margin: 12px 0 0 12px;
          line-height: 24px;
          font-size: 10px;
        }
      }
      .right{
        flex:0 0 105px;
        width:105px;
        background: #2b333b;
        text-align: center;
        .minPrice{
          height: 48px;
          line-height: 48px;
          font-size: 12px;
          font-weight: 700;

        }

      }
    }
  }
</style>
