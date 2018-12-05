<template>
  <div class="cart-ctrol">
    <div class="cart-decrease" v-show="food.count>0" @click.stop="decrease">
      <span class="inner icon-remove_circle_outline icon"></span>
    </div>
    <div class="sum" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle icon"  @click.stop="add"></div>
  </div>  
</template>

<script>
export default {
  props:{
    food: {
      type: Object
    }
  },
  methods:{
    add(){
      if(!this.food.count){
        this.$set(this.food,'count',1)
      }else{
        this.food.count++
      }
    },
    decrease(){
      if(this.food.count){
        this.food.count--
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~common/stylus/variable'
.cart-ctrol
  display: flex
  align-items: center
  .icon
    line-height: 24px
    font-size: 24px
    color: $color-blue
  .sum
    width: 24px
    line-height: 24px
    text-align: center
    font-size: 10px
    color: rgb(147,153,159)
</style>
