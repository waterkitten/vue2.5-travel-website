<template>
  <div class="header">
    城市选择
    <router-link to="/">
      <div class="iconfont header-back">&#xe624;</div>
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'CityHeader'
}
</script>
<style scoped lang='stylus'>/* 局部 */
@import '~css/var.stylus'
.header
  position relative
  overflow hidden
  height $headerHeight
  line-height $headerHeight
  background #FFA500
  text-align center
  color #fff
  font-size 0.4rem
  .header-back
    position absolute
    top 0
    left 0 0.5rem
    width 0.64rem
    text-align center
    font-size 0.4rem
    color #fff
</style>