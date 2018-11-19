<template>
  <div class="star" :class="starType">
    <span v-for="(item,index) in starCls" :class="item" class="item" :key="index"></span>
  </div>
</template>

<script>
const LENGTH=5;
const ClS_ON='on';
const ClS_HALF='half';
const ClS_OFF='off';

export default{
  props: {
    score: {
      type: Number
    },
    size: {
      type: size
    }
  },
  computed: {
    starType() {
      return 'star-'+ this.size;
    },
    starCls() {
      let result=[];
      const score= Math.floor(this.score*2)/2;
      const half= score % 1 !==0;
      const light= Math.fllor(score);
      for(let i=0; i<light; i++){
        result.push( CLS_ON )
      }
      if( half ){
        result.push( ClS_HALF )
      }
      while(result.length<LENGTH){
        result.push( ClS_OFF )
      }
      return result
    }
  }
}
</script>

<style lang="stylus" scoped>

</style>
