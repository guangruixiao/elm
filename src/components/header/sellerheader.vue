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
      <div class="bulletin">
        <span class="bulletin-icon"></span>
        <span class="bulletin-text"> {{sellerMessage.bulletin}}</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
      <div class="background">
        <img v-bind:src=sellerMessage.avatar width="100%" height="100%">
      </div>

     </div>
</template>
<script>
export default {
  props:["sellerMessage"],
  created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },

}
</script>
<style lang="scss" scoped>

 @import '../../common/scss/_mixin.scss';

  .sellerheader{
    position: relative;
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
  }
</style>
