<template>
  <div class="header">
    <div class="header-left">
      <div class="iconfont back-icon">&#xe624;</div>
    </div>
    <div class="header-input">
      <span class="iconfont">&#xe632;</span>
      输入城市/景点/游玩主题
    </div>
    <router-link to='/city'>
      <div class="header-right">
        {{this.$store.state.city}}
        <span class="iconfont arrow-icon">&#xe64a;</span>
      </div>
    </router-link>
  </div>
</template>

<script>

export default {
  name: 'HomeHeader'
  
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.header
    display: flex
    line-height: $headerHeight
    background-color: $bgColor
    color: #fff 
    .header-left
        width: 0.64rem
        .back-icon
            font-size: .4rem
            text-align: center
    .header-input
        flex: 1
        height: .64rem
        line-height :.64rem
        margin-top: .12rem
        margin-left: .2rem
        padding-left: .2rem
        background: #fff
        border-radius: .1rem
        color: #ccc
    .header-right
        min-width: 1.04rem
        color: #ffffff
        padding: 0 .1rem
        text-align: center
        .arrow-icon
            margin-left: -0.05rem
            font-size .24rem

  
</style>
