<template>
  <div class="cart-shop">
    <div class="cart-wrap">
      <div class="left-info">
        <div class="logo-wrap">
          <div class="logo">
            <i class="icon-shopping_cart"></i>
          </div>
        </div>
        <div class="price">￥0</div>
        <div class="desc">另需配送费￥4元</div>
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
      show:false
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~common/stylus/variable'

.cart-shop
  background: $clor-dark1
  height: 48px
  .cart-wrap
    display: flex
    .left-info
      flex:1
      display: flex
      .logo-wrap
        position: relative
        z-index: 999
        top: -10px
        left: 12px
        width: 56px
        height: 56px
        border-radius: 50%
        background: #08121c
        padding: 6px
        box-sizing: border-box
        .logo
          width: 44px
          height: 44px
          border-radius: 50%
          background: #2b343c
          color: #80858a
          font-size: 20px
          line-height: 44px
          text-align: center
      .price
        line-height: 48px
        margin: 0 12px
        font-size: 16px
        color: #919396
        font-weight: bold
      .desc
        height: 24px
        line-height: 24px
        margin: 12px 0
        padding-left: 12px
        border-left: 1px solid #2c343d
        color: #72777d
        font-size: 10px
    .deliver
      width: 105px
      height: 48px
      line-height: 48px
      text-align: center
      background: #2b333b
      color: #808589
      font-size: 12px
      font-weight: bold

</style>

