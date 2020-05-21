<template>
  <div>
    <div class="banner">
      <img class="banner-img"
           src="http://img1.qunarzz.com/sight/p0/1505/be/be4802e10f3b3107.water.jpg_600x330_9eb9410c.jpg"
           alt="">
      <div class="banner-info">
        <div class="banner-title">
          武隆天坑地缝国家地质公园
        </div>
        <div class="banner-number">
          <span class="iconfont icon-tupian">&#xea9c;</span>
          3
        </div>
      </div>
    </div>

  </div>
</template>

<script>

export default {
  name: 'DetailBanner'

}
</script>

<style lang="stylus" scoped>
.banner
  position relative
  overflow hidden
  height 0
  padding-bottom 55%
  .banner-img
    width 100%
  .banner-info
    display flex
    position absolute
    left 0
    right 0
    bottom 0
    line-height 0.6rem
    color #fff
    background-image linear-gradient(top, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.8)) // 从底部渐变
    .banner-title
      flex 1
      font-size 0.32rem
      padding 0 0.2rem
    .banner-number
      padding 0 0.4rem
      height 0.32rem
      line-height 0.32rem
      margin-top 0.14rem
      font-size 0.24rem
      border-radius 0.2rem
      background rgba(0, 0, 0, 0.8)
      .iconfont
        font-size 0.24rem
</style>
