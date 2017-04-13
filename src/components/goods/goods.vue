<template>
     <div class="goods">
      <div class="menubar">
        <ul class="menubar-list">
          <li class="menubar-item" v-for="item in goodsinfo">
            <span class="menubar-name">{{item.name}}</span>
          </li>
        </ul>
      </div>
      <div class="content"></div>
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

  .goods{
    display:flex;
    position:absolute;
    top:174px;
    bottom:50px;
    width:100%;
    overflow:hidden;
    .menubar{
      flex: 0 0 80px;
      width:80px;
      background:#f3f5f7;
      .menubar-item{
        display: table;
        height: 54px;
        width: 56px;
        padding: 0 12px;
        font-size:12px;
        line-height:14px;
        font-weight:200;
        .menubar-name{
          display: table-cell;
          width: 56px;
          vertical-align: middle;

        }
      }
    }
    .content{
      flex:1;
    }
  }
</style>
