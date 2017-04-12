<template>
     <div>
      <span class="on">{{scorenum[0]}}</span>
      <span class="half"></span>
      <span class="off"></span>
    </div>
</template>
<script>
export default {
  props:["score"],
  data() {
    return {
      scorenum: []
    };
  },
  mounted(){
      this.computenum();

    },
  methods:{
    computenum:function(){
      this.scorenum[0]=parseInt(this.score)


    }
  }

}

</script>
<style>
</style>
