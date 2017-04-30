<template>
    <div class="carfooter">
      <div class="content">
        <div class="left">
          <span class="logo-wrapper">
            <i class="icon-shopping_cart" ></i>
          </span>
          <span class="totalCount" v-if="totalCount>0">{{totalCount}}</span>
          <span class="totalPrice">￥{{totalPrice}}</span>
          <span class="desc">另需配送费{{deliveryPrice}}￥</span>
        </div>
        <div class="right">
          <span class="minPrice">{{check}}</span>
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
      },
      selectFoods:{},
  },
  data() {
    return {

    };
  },

  computed:{
    totalCount() {
            let count = 0;
            this.selectFoods.forEach((food) => {
              count += food.count;
            });
            return count;
          },

    totalPrice() {
            let total = 0;
            this.selectFoods.forEach((food) => {
              total += food.price * food.count;
            });
            return total;
          },
    check() {
          if(this.totalPrice >= this.minPrice){
            return "去结算"
          }else if(this.totalPrice>0){
            let gapPrice=this.minPrice-this.totalPrice;
            return "还差￥"+gapPrice+"起送"
          }else{
            return "￥"+this.minPrice+"起送"
          }
    }
  }

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
        position:relative;
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
        .totalCount{
          position:absolute;
          left:48px;
          width:24px;
          top:-8px;
          background-color:rgb(240,20,20);
          box-shadow:0px 2px 4px 0px rgba(0,0,0,0.4);
          border-radius:6px;
          text-align:center;
          font-size:9px;
          font-weight:700;
          color:rgb(255,255,255);
          line-height:16px;
        }
        .totalPrice{
          display: inline-block;
          margin-top: 12px;
          line-height: 24px;
          padding-right: 12px;
          box-sizing: border-box;
          border-right: 1px solid rgba(255, 255, 255, 0.1);
          font-size: 16px;
          font-weight: 700;
          color:rgb(255,255,255);
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
