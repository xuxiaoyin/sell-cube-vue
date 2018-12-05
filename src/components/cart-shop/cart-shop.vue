<template>
  <div class="cart-shop">
    <div class="cart-wrap">
      <div class="left-info">
        <div class="logo-wrap">
          <div class="logo" :class="{'highlight':totalPrice>0}">
            <i class="icon-shopping_cart"></i>
          </div>
          <div v-show="totalCount>0" class="num">{{totalCount}}</div>
        </div>
        <div class="price" :class="{'highlight':totalPrice>0}">￥{{totalPrice}}</div>
        <div class="desc">另需配送费￥4元</div>
      </div>
      <div class="deliver">
        <div class="normal" v-if="totalPrice===0">￥{{minPrice}}起送</div>
        <div class="normal" v-if="totalPrice<minPrice">还差￥{{minPrice-totalPrice}}起送</div>
        <div class="active" v-if="totalPrice>=minPrice">去结算</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    selectFood: {
      type: Array,
      default() {
          return []
      }
    },
    minPrice: {
      type: Number,
      default: 0
    },
    deliveryPrice: {
      type: Number,
      default: 0
    }
  },
  computed:{
    totalPrice(){
      let total=0;
      this.selectFood.forEach((food)=>{
        total+=food.count*food.price
      })
      return total
    },
    totalCount(){
      let total=0;
      this.selectFood.forEach((food)=>{
        total+=food.count
        return total
      })
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
          &.highlight
            background: #00a0dc
            color: #fff
        .num
          position: absolute 
          top: 0
          right: 0
          padding: 0 5px
          height: 16px
          width: 13px
          line-height: 16px
          text-align: center
          color: #fff
          background: #f01414
          border-radius: 16px
          font-family: Helvetica
          font-weight: 700
          font-size: 9px
          box-shadow: 4px 0 8px rgba(0,0,0,.4) 
      .price
        line-height: 48px
        margin: 0 12px
        font-size: 16px
        color: #919396
        font-weight: bold
        &.highlight
         color: #fff
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
      .active
        background: #00b43c
        color: #fff
</style>

