<template>
     <div>
      <router-link class="link" to="/goods">商品</router-link>
      <router-link class="link" to="/comment">评价</router-link>
      <router-link class="link" to="/seller">商家</router-link>
    </div>
</template>
<script>
</script>

<style  lang="scss" scoped>
  .link {
    flex:1;
    display:block;        /*让链接可以在整个区块被点击*/
    text-align:center;
    font-size:14px;
    color:rgb(77,85,93);
  }
  .active {color:rgb(240,20,20);}
</style>
