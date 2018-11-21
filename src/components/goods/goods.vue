<template>
  <div class="goods">
    <div class="scroll-nav-wrapper">
      <cube-scroll-nav
        :side="true"
        :data="goods"
        v-if="goods.length"
        :options="scrollOptions"
        @change="changeHandler"
        @sticky-change="stickyChangeHandler">
        <cube-scroll-nav-panel
          v-for="item in goods"
          :key="item.name"
          :label="item.name"
          :title="item.name">
          <ul class="food-wrap">
            <li v-for="food in item.foods" :key="food.name" class="food border-bottom-1px">
              <div class="food-detail">
                <img :src="food.icon" width="57" height="57" class="pic">
                <div class="text">
                  <div class="name">{{food.name}}</div>
                  <div class="description" v-if="food.description">{{food.description}}</div>
                  <div class="info">
                    <span class="sellCount">{{food.sellCount}}</span>
                    <span class="rating">{{food.rating}}%</span>
                  </div>
                  <div class="price-info">
                    <span class="price"><mark>￥</mark>{{food.price}}</span>
                    <span class="oldPrice" v-if="food.oldPrice"><mark>￥</mark>{{food.oldPrice}}</span>
                  </div>
                </div>
              </div>
            </li>
          </ul>
        </cube-scroll-nav-panel>
      </cube-scroll-nav>
    </div>
  </div>
</template>

<script>
import {getGoods} from 'api'
import SupportIcon from 'components/support-icon/support-icon'

export default {
  props:{
    data:{
      type:Object,
      default(){
        return{}
      }
    }
  },
  data() {
    return{
      goods:[],
      scrollOptions:{
        click:false,
        directionLockThreshold:0
      }
    }
  },
  methods: {
    changeHandler(label) {
      console.log('changed to:', label)
    },
    stickyChangeHandler(current) {
      console.log('sticky-change', current)
    },
    fetch(){
      getGoods().then(goods=>{
        this.goods=goods
      })
    }
  },
  components:{
    SupportIcon
  }
}
</script>

<style lang="stylus" scoped>
@import '~common/stylus/variable'
@import '~common/stylus/mixin'

.border-bottom-1px
  border-1px($color-row-line)

.goods
  position: relative
  text-align: left 
  height: 100%
  .scroll-nav-wrapper
    position: absolute 
    left:0
    top:0
    right:0
    bottom: 48px
   >>>.cube-scroll-nav-bar
    width: 80px
    white-space: normal
    overflow: hidden 
  >>>.cube-scroll-nav-bar-item
    padding:0 12px
    display: flex
    align-items: center
    height: 54px
    line-height: 14px
    font-size: 12px
    background: $background-dark4
    color: $clor-dark1
    font-weight: 200
  >>>.cube-scroll-nav-bar-item_active
    background: #fff
    color: #000
  >>>.cube-scroll-nav-panel-title
    height: 26px
    padding-left: 12px
    background: $background-dark4
    font-size: 12px
    color: rgb(147,153,159)
    line-height: 26px
    border-left: 2px solid #d9dde1

  .food-wrap
    paddign-right: 18px
    .food
      padding: 18px 0 18px 18px
      .food-detail
        display: flex
        .pic
          display: block
          border-radius: 2px
          width: 57px
          height: 57px
          overflow: hidden
          margin-right: 10px
        .text
          flex：1
          .name
            line-height: 14px
            margin-right: 2px
            margin-bottom: 8px
            font-size: 14px
            color: rgb(7,17,27)
          .description,.info
            line-height: 10px
            margin-bottom: 8px
            font-size: 10px
            color: rgb(147,153,159)
          .info
            font-size:0
            span 
              display: inline-block
              font-size: 10px
              margin-right: 12px
              &.rating
               margin-right: 0
          .price-info
            font-size: 0
            span
              display: inline-block
              &.price
                line-height: 24px
                font-size: 14px
                font-weight: 700
                color:$color-red
                margin-right: 8px
                mark
                  background: none
                  font-size: 10px
                  color:$color-red
                  font-weight: 200 
              &.oldPrice
                font-size: 10px
                line-height: 24px
                color: rgb(147,153,159)
                font-weight: 700
                text-decoration: line-through
                mark
                  background: none
                  font-size: 10px
                  color:rgb(147,153,159)
                  font-weight: 200 
              


            
        
      

</style>