<template>
     <div>
      商品页
    </div>
</template>
<script>
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


}

</script>
<style  lang="scss" scoped>
</style>
