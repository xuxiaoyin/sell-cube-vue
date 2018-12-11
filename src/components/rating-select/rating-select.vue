<template>
  <div class="wrap">
      <span class="active normal">全部<span class="num">57</span></span>
      <span class="normal">推荐<span class="num">47</span></span>
      <span class="normal negative">吐槽<span class="num">2</span></span>
  </div>  
</template>

<script>
export default {
    
}
</script>

<style lang="stylus" scoped>
    .wrap
        height: 32px
        .normal
            float: left 
            margin-right: 8px
            height: 32px
            width: 60px
            line-height: 32px
            text-align: center
            border-radius: 2px
            background: #ccecf8
            font-size: 12px
            color: #4d555d
            .num
                font-size: 8px
                margin-left: 2px
            &.active
                color: #fff
                background: #00a0dc
        .negative
            background: #e9ebec
</style>
