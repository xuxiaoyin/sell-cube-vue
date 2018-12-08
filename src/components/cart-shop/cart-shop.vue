<template>
  <div class="cart-shop">
    <div class="cart-wrap">
      <div class="left-info">
        <div class="logo-wrap">
          <div class="logo" :class="{'highlight':totalPrice>0}">
            <i class="icon-shopping_cart"></i>
          </div>
          <bubble v-show="totalCount>0" :totalCount="totalCount"></bubble> 
        </div>
        <div class="price" :class="{'highlight':totalPrice>0}">￥{{totalPrice}}</div>
        <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
      </div>
      <div class="deliver" :class="{active:totalPrice>=minPrice}">
        {{pay}}
      </div>
      <div class="ball-container">
        <div v-for="(ball,index) in balls" :key="index">
          <transition
            @before-enter="beforeDrop"
            @enter="dropping"
            @after-enter="afterDrop">
            <div class="ball" v-show="ball.show">
              <div class="inner inner-hook"></div>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Bubble from 'components/bubble/bubble'

const LENG=10;
function creatBall(){
  let balls=[];
  for( let i=0;i<LENG;i++){
    balls.push({
      show: false
    })
    return balls;
  }
}

export default {
  data() {
    return {
      balls: creatBall()
    }
  },
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
  created() {
    this.dropBalls = []
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
      })
      return total
    },
    pay(){
      if(this.totalPrice===0){
        return `￥${this.minPrice}元起送`
      }else if(this.totalPrice<this.minPrice){
        let diff=this.minPrice-this.totalPrice
        return `还差￥${diff}元起送`
      }else{
        return '去结算'
      }
    }
  },
  methods:{
    drop(el) {
      for (let i = 0; i < this.balls.length; i++) {
        const ball = this.balls[i]
        if (!ball.show) {
          ball.show = true
          ball.el = el
          this.dropBalls.push(ball)
          return
        }
      }
    },
    beforeDrop(el) {
      const ball = this.dropBalls[this.dropBalls.length - 1]
      const rect = ball.el.getBoundingClientRect()
      const x = rect.left - 32
      const y = -(window.innerHeight - rect.top - 22)
      el.style.display = ''
      el.style.transform = el.style.webkitTransform = `translate3d(0,${y}px,0)`
      const inner = el.getElementsByClassName(innerClsHook)[0]
      inner.style.transform = inner.style.webkitTransform = `translate3d(${x}px,0,0)`
    },
    dropping(el, done) {
      this._reflow = document.body.offsetHeight
      el.style.transform = el.style.webkitTransform = `translate3d(0,0,0)`
      const inner = el.getElementsByClassName(innerClsHook)[0]
      inner.style.transform = inner.style.webkitTransform = `translate3d(0,0,0)`
      el.addEventListener('transitionend', done)
    },
    afterDrop(el) {
      const ball = this.dropBalls.shift()
      if (ball) {
        ball.show = false
        el.style.display = 'none'
      }
    },
  },
  components: {
    Bubble
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
      &.active
        background: #00b43c
        color: #fff
    .ball-container
      .ball
        position: fixed
        left: 32px
        bottom: 22px
        z-index: 200
        transition: all 0.4s cubic-bezier(0.49, -0.29, 0.75, 0.41)
        .inner
          width: 16px
          height: 16px
          border-radius: 50%
          background: $color-blue
          transition: all 0.4s linear

</style>

