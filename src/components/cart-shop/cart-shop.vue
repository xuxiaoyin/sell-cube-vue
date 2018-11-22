<template>
  <div class="cart-shop">
    <div class="cart-wrap">
      <div class="left-info">

      </div>
      <div class="deliver">
        <div class="normal" v-if="!show">￥20起送</div>
        <div class="active" v-if="show">去结算</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      show:true
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~common/stylus/variable'

.cart-shop
  background: $clor-dark1
  height: 48px
</style>

