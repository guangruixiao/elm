<template>
    <div class="goods">
      <div class="menubar" ref="menuWrapper">
        <ul class="menubar-list">
          <li class="menubar-item border-1px" v-for="(item,index) in goodsinfo" :class="{'current':currentIndex===index}" @click="selectMenu(index,$event)">
            <span class="menubar-text">
              <icon class="menubar-icon" v-show="item.type>0" v-bind:size="3" v-bind:type="item.type"></icon>{{item.name}}
            </span>
          </li>
        </ul>
      </div>
      <div class="content" ref="foodsWrapper">
        <ul class="content-list">
          <li class="content-wrapper" v-for="(item,index) in goodsinfo" ref="foodList" >
            <div class="content-title">
              <span class="content-name">{{item.name}}</span>
            </div>
            <div class="content-goods border-1px" v-for="food in (item.foods)">
              <img class="food-image" width="57" height="57" v-bind:src=food.icon alt="">
              <div class="text">
                <div class="text-name">{{food.name}}</div>
                <div class="desc">{{food.description}}</div>
                <div class="extra">
                  <span class="count">月售{{food.sellCount}}份</span><span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span class="now">￥{{food.price}}</span>
                  <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}
                  </span>
                </div>
              </div>
              <selectcart class="selectVue" v-bind:food="food" ></selectcart>
            </div>
          </li>
        </ul>
      </div>
      <shoppingcar class="carfooter" v-on:cartClick="cartShow"  v-bind:selectFoods="selectFoods" v-bind:deliveryPrice="sellerMessage.deliveryPrice" v-bind:minPrice="sellerMessage.minPrice" v-bind:cartShow="cartShow"></shoppingcar>
      <transition  name="fold">
        <div class="cartDetail" v-if="cartState" >
          <div class="detail-wrapper">
              <div class="detail-title">
                <span class="name">购物车</span>
                <span v-on:click="deleteCart" class="clear">清空</span>
              </div>
              <ul class=detail-list>
                <li class="detail-goods" v-for="item in selectFoods">
                  <div class="detail-good">
                    <span class="good-name">{{item.name}}</span>
                    <span class="good-price">{{item.price*item.count}}</span>
                    <selectcart v-bind:food="item" class="detail-select" ></selectcart>
                  </div>
                </li>
              </ul>
          </div>
        </div>
      </transition>
    </div>
</template>
<script>
import icon from '../icon/icon';
import BScroll from 'better-scroll'
import shoppingcar from '../shoppingcarfooter'
import selectcart from '../select'
import Vue from 'vue';


export default {
  props:["sellerMessage"],
  data:function(){
        return {goodsinfo:[], listHeight: [], scrollY: 0,cartState:false}
    },
  created(){
      this.fetchdata();
    },

  computed: {
        currentIndex() {
          for (let i = 0; i < this.listHeight.length; i++) {
            let height1 = this.listHeight[i];
            let height2 = this.listHeight[i + 1];
            if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
              return i;
            }
          }
          return 0;
        },
        selectFoods() {
                let foods = [];
                this.goodsinfo.forEach((good) => {
                  good.foods.forEach((food) => {
                    if (food.count) {
                      foods.push(food);
                    }
                  });
                });
                return foods;
              }
  },
  methods:{
      fetchdata:function(){
        var self=this;
        this.$http.get('/api/goods')
         .then(function (response) {
            self.goodsinfo=response.data.data;
            self.$nextTick(() => {
              self._initScroll();
              self._calculateHeight();
            })

         })
         .catch(function (response) {
           console.log("没有接收到信息");
         });
      },
      _initScroll:function(){
              this.meunScroll = new BScroll(this.$refs.menuWrapper, {
                click: true
              });

              this.foodsScroll = new BScroll(this.$refs.foodsWrapper, {
                click: true,
                probeType: 3
              });
              this.foodsScroll.on('scroll', (pos) => {
                        this.scrollY = Math.abs(Math.round(pos.y));
                      });

      },
      _calculateHeight() {
              let foodList = this.$refs.foodList;
              let height = 0;
              this.listHeight.push(height);
              for (let i = 0; i < foodList.length; i++) {
                let item = foodList[i];
                height += item.clientHeight;
                this.listHeight.push(height);
              }
      },

      selectMenu(index, event) {
              if (!event._constructed) {
                return;
              }
              let foodList = this.$refs.foodList;
              let el = foodList[index];
              this.foodsScroll.scrollToElement(el, 300);
      },

      cartShow:function(){
        if(this.cartState==false){
            this.cartState=true
        }else{
          this.cartState=false
        }
      },

      deleteCart:function(){
        this.goodsinfo.forEach((good) => {
          good.foods.forEach((food) => {
            if (food.count) {
              Vue.delete(food, 'count');
            }
          });
        });

        this.cartState=false;



      }


  },
  components: {
    icon,
    shoppingcar,
    selectcart
  }
}

</script>
<style  lang="scss" scoped>
@import '../../common/scss/_mixin';

  .goods{
    display:flex;
    position:absolute;
    top:174px;
    bottom:50px;
    width:100%;
    overflow:hidden;
    .menubar{
      flex: 0 0 80px;
      width:80px;          /*安卓兼容性*/
      background:#f3f5f7;
      .menubar-item{
        display: table;
        height: 54px;
        width: 56px;
        padding: 0 12px;
        font-size:12px;
        line-height:14px;
        font-weight:200;
        @include border-1px(rgba(7, 17, 27, 0.1))
        &.border-1px{
          &:after{
            left: 12px;
            width: 56px;
          }
        }
        &.current{
          position: relative;
          z-index: 10;
          margin-top: -1px;
          background: #fff;
          font-weight: 700;
        }
        .menubar-icon{
          vertical-align: top;
        }
        .menubar-text{
          display: table-cell;
          width: 56px;
          vertical-align: middle;
        }
      }
    }
    .content{
      flex:1;
      .content-wrapper{
        .content-title{
          height:26px;
          background-color:#f3f5f7;
          border-left: 2px solid #d9dde1;
          .content-name{
            margin-left:14px;
            font-size:12px;
            color:rgb(147,153,159);
            line-height:26px;
          }
        }
        .content-goods{
          display: flex;
          position:relative;
          margin: 18px;
          padding-bottom: 18px;
          @include border-1px(rgba(7, 17, 27, 0.1));
          .food-image{
            flex: 0 0 57px;
          }
          .text{
            flex: 1;
            display: inline-block;
            margin-left: 10px;
            .text-name{
              margin: 2px 0 8px 0;
              height: 14px;
              line-height: 14px;
              font-size: 14px;
              color: rgb(7, 17, 27);
            }
            .desc, .extra{
              line-height: 10px;
              font-size: 10px;
              color: rgb(147, 153, 159);
            }
            .desc{
              line-height: 12px;
              margin-bottom: 8px;
            }
            .extra{
              .count{
                margin-right: 12px
              }
            }
            .price{
              font-weight: 700;
              line-height: 24px;
              .now{
                  margin-right: 8px;
                font-size: 14px;
                color: rgb(240, 20, 20);
              }
              .old{
                text-decoration: line-through;
                font-size: 10px;
                color: rgb(147, 153, 159);
              }

            }
          }

        }
      }
    }
    .cartDetail{
        position:fixed;
        z-index:3;
        left:0;
        top:0;
        width:100%;
        height:100%;
        background-color:rgba(7,17,27,0.8);
        transform: translate3d(0, 0, 0);
        &.fold-enter-active, &.fold-leave-active{
          transition: all 1.2s
        }
        &.fold-enter, &.fold-leave-active{
          transform: translate3d(0, 100%, 0)
        }
        .detail-wrapper{
          position: absolute;
          left: 0;
          bottom: 54px;
          width:100%;

          .detail-title{
            height:40px;
            line-height: 24px;
            font-size: 18px;
            color: rgb(7, 17, 27);
            background-color:#f3f5f7;
            .name{
              display:inline-block;
              margin-top:10px;
              margin-left:12px;
            }
            .clear{
              display:inline-block;
              margin-top:10px;
              margin-left:228px;
            }

          }
          .detail-list{
            max-height:265px;
            overflow:auto;
            .detail-goods{
              padding: 12px 0;
              background-color:white;
              height:48px;
              position:relative;
              .good-name{
                display:inline-block;
                margin-left:12px;
              }
              .good-price{
                display:inline-block;
                position:absolute;
                left:160px;
                color:red;
              }
              .detail-select{
                bottom:0;
                padding-right: 18px;
                font-size:18px;
                font-weight:700;
              }
            }
          }
        }

      }


  }
</style>
