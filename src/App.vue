<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
  </div>
</template>

<script>
import VHeader from 'components/v-header/v-header'
import {getSeller} from 'api'

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
    VHeader
  }
}
</script>
<style lang="stylus" rel="stylesheet/stylus">

</style>
