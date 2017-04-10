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
            <span class="icon" v-bind:class="classMap[sellerMessage.supports[0].type]"></span>
            <span class="text">{{sellerMessage.supports[0].description}}</span>
            <span class="count">{{sellerMessage.supports.length}}个</span>
          </div>
        </div>
      </div>
      <div class="bulletin">{{sellerMessage.bulletin}}</div>
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
          margin-top:10px;
          .icon{
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
          .text{
            display:inline-block;
            vertical-align:bottom;
            margin-left:4px;
            line-height: 12px;
            font-size: 10px;
          }

        }
      }



    }
  }
</style>
