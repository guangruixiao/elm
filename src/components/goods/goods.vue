<template>
    <div class="goods">
      <div class="menubar">
        <ul class="menubar-list">
          <li class="menubar-item border-1px" v-for="item in goodsinfo">
            <span class="menubar-text">
              <icon class="menubar-icon" v-show="item.type>0" v-bind:size="3" v-bind:type="item.type"></icon>{{item.name}}
            </span>
          </li>
        </ul>
      </div>
      <div class="content">
        <ul class="content-list">
          <li class="content-wrapper" v-for="item in goodsinfo">
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
            </div>
          </li>
        </ul>
      </div>
    </div>
</template>
<script>
import icon from '../icon/icon'


export default {

  data:function(){
        return {goodsinfo:[]}
    },
  mounted(){
      this.fetchdata();
    },
  methods:{
      fetchdata:function(){
        var self=this;
        this.$http.get('/api/goods')
         .then(function (response) {
            self.goodsinfo=response.data.data;
         })
         .catch(function (response) {
           console.log("没有接收到信息");
         });
      }
    },
  components: {
    icon
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
</style>
