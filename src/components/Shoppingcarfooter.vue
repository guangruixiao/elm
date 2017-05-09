<template>
    <div class="carfooter">
      <div class="content">
        <div class="left" v-on:click="cartClick">
          <span class="logo-wrapper">
            <i class="icon-shopping_cart" ></i>
          </span>
          <span class="totalCount" v-if="totalCount>0">{{totalCount}}</span>
          <span class="totalPrice">￥{{totalPrice}}</span>
          <span class="desc">另需配送费{{deliveryPrice}}￥</span>
        </div>
        <div class="right"  v-bind:class="{ check: isActive }">
          <span class="minPrice">{{check}}</span>
        </div>
      </div>
      <div class="ball-container">
        <div v-for="ball in balls">
          <transition name="drop" @before-enter="beforeDrop" @enter="dropping" @after-enter="afterDrop">
            <div class="ball" v-show="ball.show">
                <div class="inner inner-hook"></div>
            </div>
          </transition>
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
      cartShow:{}
  },
  data() {
    return {
      isActive:false,
      balls: [
                {
                  show: false
                },
                {
                  show: false
                },
                {
                  show: false
                },
                {
                  show: false
                },
                {
                  show: false
                }
              ],
      dropBalls: [],

    };
  },
  created(){
      this.$root.$on('add',(target) => {
      this.drop(target)
    });
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
            this.isActive=true;
            return "去结算"
          }else if(this.totalPrice>0){
            this.isActive=false;
            let gapPrice=this.minPrice-this.totalPrice;
            return "还差￥"+gapPrice+"起送"
          }else{
            this.isActive=false;
            return "￥"+this.minPrice+"起送"
          }
    },
  },

  methods:{
    cartClick:function() {
      if(this.totalPrice >= this.minPrice){
         this.$emit('cartClick')
      }
    },
    drop(el) {
           for (let i = 0; i < this.balls.length; i++) {
             let ball = this.balls[i];
             if (!ball.show) {
               ball.show = true;
               ball.el = el;
               this.dropBalls.push(ball);
               return;
             }
           }
         },
    beforeDrop(el) {
      let count = this.balls.length;
      while (count--) {
        let ball = this.balls[count];
        if (ball.show) {
          let rect = ball.el.getBoundingClientRect();
          let x = rect.left - 32;
          let y = -(window.innerHeight - rect.top - 22);
          el.style.display = '';
          el.style.webkitTransform = `translate3d(0,${y}px,0)`;
          el.style.transform = `translate3d(0,${y}px,0)`;
          let inner = el.getElementsByClassName('inner-hook')[0];
          inner.style.webkitTransform = `translate3d(${x}px,0,0)`;
          inner.style.transform = `translate3d(${x}px,0,0)`;
        }
      }
    },
    dropping(el, done) {
      /* eslint-disable no-unused-vars */
      let rf = el.offsetHeight;
      this.$nextTick(() => {
        el.style.webkitTransform = 'translate3d(0,0,0)';
        el.style.transform = 'translate3d(0,0,0)';
        let inner = el.getElementsByClassName('inner-hook')[0];
        inner.style.webkitTransform = 'translate3d(0,0,0)';
        inner.style.transform = 'translate3d(0,0,0)';
        el.addEventListener('transitionend', done);
      });
    },
    afterDrop(el) {
      let ball = this.dropBalls.shift();
      if (ball) {
        ball.show = false;
        el.style.display = 'none';
      }
    },

  }




}
</script>
<style lang="scss" scoped>
  .carfooter{
    position:fixed;
    bottom:0;
    left:0;
    z-index:50;
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
        &.check{
            background: green;
            color:rgb(255,255,255);
          }
        .minPrice{
          height: 48px;
          line-height: 48px;
          font-size: 12px;
          font-weight: 700;


        }

      }
    }
    .ball-container{
      .ball{
        position: fixed;
        left: 32px;
        bottom: 22px;
        z-index: 200;
        transition: all 0.6s cubic-bezier(0.49, -0.29, 0.75, 0.41);
        .inner{
          width: 17px;
          height: 17px;
          border-radius: 50%;
          background: rgb(0, 160, 220);
          transition: all 0.6s linear;
        }
      }
    }
  }
</style>
