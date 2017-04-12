<template>
    <div class="sellerheader">
      <div class="content-wrapper">
        <img class="avatar" width="64" height="64" v-bind:src=sellerMessage.avatar alt="">
        <div class="content">
          <div class="title">
            <span class="brand"></span>
            <span class="name">{{sellerMessage.name}}</span>
          </div>
          <div class="description">{{sellerMessage.description}}/{{sellerMessage.deliveryTime}}分钟送达</div>
          <div class="supports" v-if=sellerMessage.supports>
            <span class="supports-icon" v-bind:class="classMap[sellerMessage.supports[0].type]"></span>
            <span class="supports-text">{{sellerMessage.supports[0].description}}</span>
            <span class="supports-count">{{sellerMessage.supports.length}}个</span>
            <i class="icon-keyboard_arrow_right"></i>
          </div>
        </div>
      </div>
      <div class="bulletin"  v-on:click="sellerlistshow" >
        <span class="bulletin-icon"></span>
        <span class="bulletin-text"> {{sellerMessage.bulletin}}</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
      <div class="background">
        <img v-bind:src=sellerMessage.avatar width="100%" height="100%">
      </div>
      <div class="detail" v-show="sellerdetail" >
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <div class="detail-header">
              <h1 class="detail-name">{{sellerMessage.name}}</h1>
              <star class="detail-star" v-bind:score="(sellerMessage.score)"></star>
            </div>
            <div class="detail-title">
              <span>优惠信息</span>
            </div>
            <div class="detail-supports" v-for="item in (sellerMessage.supports)">
              <span class="detail-icon" v-bind:class="classMap[item.type]"></span>
              <span class="detail-description">{{item.description}}</span>
            </div>
            <div class="detail-title">
              <span>商家公告</span>
            </div>
            <div class="detail-bulletin">
              <p>{{sellerMessage.bulletin}}</p>
            </div>
          </div>
        </div>
        <div class="detail-close" v-on:click="sellerlistshow">
          <i class="icon-close"></i>
        </div>
      </div>
    </div>
</template>
<script>
import star from '../star/star'

export default {
  props:["sellerMessage"],
  data() {
    return {
      sellerdetail: false
    };
  },
  created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
  methods:{
    sellerlistshow:function(){
      if(this.sellerdetail==false){
        this.sellerdetail=true;
      }else{
        this.sellerdetail=false;
      }
    }
  },
  components: {
    star
  }
}
</script>
<style lang="scss" scoped>
 @import '../../common/scss/_mixin.scss';
  .sellerheader{
    position: relative;
    overflow:hidden;
    color:white;
    background-color:rgba(7,17,27,0.5);
    blur:10px;
    .content-wrapper{
      position:relative;
      width:100%;
      height:106px;
      .avatar{
        margin-left:24px;
        margin-top:24px;
        border-radious:2px;
      }
      .content{
        position:absolute;
        left:104px;
        top:26px;
        .title{
          .brand{
            display:inline-block;
            vertical-align: top;
            width:30px;
            height:18px;
            @include bg-image("brand");
            background-size: 30px 18px;
            background-repeat: no-repeat;
          }
          .name{
            margin-left: 6px;
            font-size: 16px;
            line-height: 18px;
            font-weight: bold;
          }
        }
        .description{
          margin-top:8px;
          line-height: 12px;
          font-size: 12px;
        }
        .supports{
          font-size: 0;
          margin-top:10px;
          .supports-icon{
            display:inline-block;
            vertical-align:bottom;
            width: 12px;
            height: 12px;
            background-size: 12px 12px;
            background-repeat: no-repeat;
            &.decrease{
             @include bg-image('decrease_1')
            }
            &.discount{
             @include bg-image('discount_1')
            }
            &.guarantee{
             @include bg-image('guarantee_1')
            }
            &.invoice{
             @include bg-image('invoice_1')
            }
            &.special{
            @include bg-image('special_1')
            }
          }
          .supports-text{
            vertical-align:bottom;
            margin-left:4px;
            line-height: 12px;
            font-size: 10px;
          }
          .supports-count{
            margin-left:100px;
            vertical-align: bottom;
            font-size: 10px;
          }
          .icon-keyboard_arrow_right{
            margin-left:1px;
            font-size: 10px;
          }
        }
      }
    }
    .bulletin{
      position: relative;
      height:28px;
      padding: 0 24px 0 12px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      background-color:rgba(7,17,27,0.2);
      .bulletin-icon{
        display:inline-block;
        vertical-align: middle;
        width:22px;
        height:12px;
        @include bg-image("bulletin");
            background-size: 22px 12px;
            background-repeat: no-repeat;
      }
      .bulletin-text{
        margin: 0 4px;
        line-height:28px;
        font-size:10px;
        color:rgb(255,255,255);
      }
      .icon-keyboard_arrow_right{
        position: absolute;
        font-size: 10px;
        right: 8px;
        top: 8px;
      }
    }
    .background{
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      filter: blur(10px);
    }
    .detail{
      position:fixed;
      left:0;
      top:0;
      z-index: 100;
      width:100%;
      height:100%;
      overflow:auto;
      background-color:rgba(7,17,27,0.8);
      .detail-wrapper{
        width: 100%;
        min-height: 100%;
        .detail-main{
          margin-top: 64px;
          margin-left:36px;
          width:303px;
          border: 1px solid red;
          padding-bottom: 64px;
          .detail-header{
            text-align:center;
            .detail-name{
              display:inline-block;
              padding:0 auto;
              font-size:16px;
              line-height:16px;
              font-weight:700;
              color:rgb(255,255,255)
            }
            .detail-star{
              margin-top:16px;
            }
          }
          .detail-title{
            margin-top:28px;
            font-size:14px;
            line-height:14px;
            font-weight:700;
            color:rgb(255,255,255)
          }
          .detail-supports{
            margin-top:24px;
            padding-left:12px;
            .detail-icon{
              display:inline-block;
              vertical-align: middle;
              width: 16px;
              height: 16px;
              background-size: 16px 16px;
              background-repeat: no-repeat;
              &.decrease{
               @include bg-image('decrease_1')
              }
              &.discount{
               @include bg-image('discount_1')
              }
              &.guarantee{
               @include bg-image('guarantee_1')
              }
              &.invoice{
               @include bg-image('invoice_1')
              }
              &.special{
              @include bg-image('special_1')
              }
            }
            .detail-description{
              display:inline-block;
              vertical-align: middle;
              margin-left:6px;
              font-size:12px;
              line-height:12px;
              font-weight:200;
              color:rgb(255,255,255);
            }
          }
          .detail-bulletin{
            margin-top:24px;

          }

        }

      }
      .detail-close{
        position: relative;
        width: 32px;
        height: 32px;
        margin: -64px auto 0 auto;
        clear: both;
        font-size: 32px;
      }

    }

  }
</style>
