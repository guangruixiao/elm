<template>
    <div class="select">
      <span class="icon-remove_circle_outline" v-if="food.count>0" v-on:click="deleteNum"></span>
      <span class="select-num" v-if="food.count>0">{{food.count}}</span>
      <span class="icon-add_circle" v-on:click="addNum"></span>
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
    addNum:function(){
      if (!this.food.count) {
        console.log("yes")
        Vue.set(this.food, 'count', 1);
      } else {
        this.food.count++;
      }
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
    font-size:0;
    .icon-remove_circle_outline,.icon-add_circle{
      dispaly:inline-block;

      font-size:24px;
      color:rgb(0,160,220);
      line-height:24px;
    }
    .select-num{
      dispaly:inline-block;
      vertail-align:middle;
      font-size:10px;
      width:24px;
      color:rgb(147,153,159);
    }
  }

</style>
