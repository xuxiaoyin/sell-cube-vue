<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab-wrap">
      <tab></tab>
    </div> 
  </div>
</template>

<script>
import VHeader from 'components/v-header/v-header'
import {getSeller} from 'api'
import Tab from 'components/tab/tab'

export default {
  data(){
    return {
      seller: {}
    }
  },
  created(){
    getSeller().then( (seller) =>{
      this.seller=seller
    })
  },
  components:{
    VHeader,
    Tab
  }
}
</script>
<style lang="stylus" rel="stylesheet/stylus">
#app
  .tab-wrap
    position: fixed;
    top: 134px
    left: 0
    bottom: 0
    right: 0
</style>
