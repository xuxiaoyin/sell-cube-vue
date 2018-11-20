<template>
  <div class="tab">

    <cube-tab-bar v-model="selectedLabel" show-slider class="border-bottom-1px">
      <cube-tab v-for="(item, index) in tabs"  :label="item.label" :key="index">
      </cube-tab>
    </cube-tab-bar>

    <div class="slid-wrap">
      <cube-slide
        :loop="false"
        :auto-play="false"
        :show-dots="false"
        :initial-index=index
        ref="slide"
      >
        <cube-slide-item>
          <goods></goods>
        </cube-slide-item>
        <cube-slide-item>
          <ratings></ratings>
        </cube-slide-item>
        <cube-slide-item>
          <seller></seller>
        </cube-slide-item>
      </cube-slide>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import Goods from 'components/goods/goods'
import Ratings from 'components/ratings/ratings'
import Seller from 'components/seller/seller'
 export default {
  data () {
    return {
      index: 0,
      tabs: [{
        label: '商品'
      }, {
        label: '评价'
      }, {
        label: '商家'
      }]
    }
  },
  computed: {
    selectedLabel: {
      get(){
        return this.tabs[this.index].label
      },
      set(newVal){
        return this.index=this.tabs.findIndex((value)=>{
          return value.label===newVal
        })
      }
    }
  },
  components: {
    Goods,
    Ratings,
    Seller
  }
}
</script>

<style lang="stylus" scoped>
@import "~common/stylus/mixin"
@import "~common/stylus/variable"
.border-bottom-1px
  border-1px($color-row-line)

>>>.cube-tab
  padding 10px 0
</style>