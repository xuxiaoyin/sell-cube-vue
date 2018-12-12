<template>
  <cube-scroll ref="scroll" class="seller-wrap" :options="scrollOptions">
    <div class="seller">
      <div class="overview">
        <div class="title">
          <h1 class="name">{{seller.name}}</h1>
          <div class="info">
            <star :size=2 :score="seller.score" class="star"></star>
            <span class="ratingcount" v-show="seller.ratingCount">({{seller.ratingCount}})</span>
            <span class="sellcount" v-show="seller.sellCount">月售{{seller.sellCount}}单</span>
          </div>
          <div class="collect">
            <span></span>
            <span>已收藏</span>
          </div>
        </div>
      </div>
    </div>
  </cube-scroll>
</template>

<script>
import Star from 'components/star/star'
export default {
  props: {
    data: {
      type: Object,
      default(){
        return {}
      }
    }
  },
  data() {
    return {
      scrollOptions: {
        click: false,
        directionLockThreshold: 0
      }
    }
  },
  computed: {
    seller(){
      return this.data.seller
    }
  },
  components: {
    Star
  }
}
</script>

<style lang="stylus" scoped>
.seller-wrap
  position: relative
  width: 100%
  height: 100%
  .overview
    padding: 9px 18px 20px 18px
</style>
