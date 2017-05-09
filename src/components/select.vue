<template>
    <div class="select">
     <transition name="move">
       <span  class="cart-decrease" v-show="food.count>0" v-on:click="deleteNum" >
         <span class="inner icon-remove_circle_outline"></span>
       </span>
     </transition>
     <span class="select-num" v-if="food.count>0">{{food.count}}</span>
     <span class="icon-add_circle" v-on:click="addNum()"></span>
    </div>
</template>
<script>

import Vue from 'vue';

export default {
  props:["food"],
  data() {
    return {
      num: 0,
    };
  },

  methods:{
    addNum:function(target){
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1);
      } else {
        this.food.count++;
      };

      this.$root.$emit('add', event.target)
    },
    deleteNum:function(){
      if (this.food.count) {
          this.food.count--;
      }
    },

  }

}

</script>
<style lang="scss" scoped>
  .select{
    position:absolute;
    right:0;
    bottom:18px;
    .cart-decrease{
      display:inline-block;
      vertical-align:middle;
      color:rgb(0,160,220);
      opacity: 1;
      transform: translate3d(0, 0, 0);
      .inner{
        display: inline-block;
        line-height: 24px;
        font-size: 24px;
        color: rgb(0, 160, 220);
        transition: all 0.4s linear;
        transform: rotate(0);
      }
      &.move-enter-active, &.move-leave-active{
        transition: all 0.2s linear;
      }
      &.move-enter, &.move-leave-active{
        opacity: 0;
        transform: translate3d(24px, 0, 0);
        .inner{
          transform: rotate(180deg);
        }
      }
    }
    .icon-add_circle{
      display:inline-block;
      vertical-align:middle;
      font-size:24px;
      color:rgb(0,160,220);
      line-height:24px;
    }
    .select-num{
      display:inline-block;
      text-align:center;
      font-size:13px;
      width:20px;
      color:rgb(147,153,159);
    }
  }

</style>
