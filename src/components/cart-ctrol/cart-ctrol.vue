<template>
  <div class="cart-ctrol">
    <div class="cart-decrease">
      <span class="inner icon-remove_circle_outline icon"></span>
    </div>
    <div class="sum">1</div>
    <div class="cart-add icon-add_circle icon" ></div>
  </div>  
</template>

<script>
export default {
  
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
