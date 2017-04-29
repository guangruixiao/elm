<template>
    <div class="select">
      <span class="icon-remove_circle_outline" v-if="num>0" v-on:click="deleteNum"></span>
      <span class="select-num" v-if="num>0">{{num}}</span>
      <span class="icon-add_circle" v-on:click="addNum"></span>
    </div>
</template>
<script>
export default {
  data() {
    return {
      num: 0,
    };
  },

  methods:{
    addNum:function(){
      this.num=this.num+1
    },
    deleteNum:function(){
      this.num=this.num-1
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
