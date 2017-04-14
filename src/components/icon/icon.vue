<template>
  <div class="icon" :class="iconSize">
    <span class="icon-item" v-bind:class="iconType"></span>
  </div>

</template>
<script>
const typeList=['decrease', 'discount', 'special', 'invoice', 'guarantee'];

export default {
  props: {
      size: {
        type: Number
      },
      type: {
        type: Number
      }
    },
  computed:{
    iconSize:function(){
      return   "icon-"+this.size
    },
    iconType:function(){
      return  typeList[this.type]
    }
  },
}

</script>
<style  lang="scss" scoped>
  @import "../../common/scss/mixin.scss";

  .icon{
     display:inline-block;
    .icon-item{
      display: inline-block;
      background-repeat: no-repeat;
    }
    &.icon-1{
      .icon-item{
        width: 12px;
        height: 12px;
        background-size: 12px 12px;
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
    }
    &.icon-2{
      .icon-item{
        width: 16px;
        height: 16px;
        background-size: 16px 16px;
        &.decrease{
         @include bg-image('decrease_2')
        }
        &.discount{
         @include bg-image('discount_2')
        }
        &.guarantee{
         @include bg-image('guarantee_2')
        }
        &.invoice{
         @include bg-image('invoice_2')
        }
        &.special{
         @include bg-image('special_2')
        }
      }
    }
    &.icon-3{
      .icon-item{
        width: 12px;
        height: 12px;
        background-size: 12px 12px;
        &.decrease{
         @include bg-image('decrease_3')
        }
        &.discount{
         @include bg-image('discount_3')
        }
        &.guarantee{
         @include bg-image('guarantee_3')
        }
        &.invoice{
         @include bg-image('invoice_3')
        }
        &.special{
         @include bg-image('special_3')
        }
      }
    }
  }

</style>
