<template>
  <div>
    <div class="banner"
         @click="handleBannerClick">
      <img class="banner-img"
           src="https://img1.qunarzz.com/sight/p0/1505/be/be4802e10f3b3107.water.jpg_600x330_9eb9410c.jpg"
           alt="">
      <div class="banner-info">
        <div class="banner-title">
          武隆天坑地缝国家地质公园
        </div>
        <div class="banner-number">
          <span class="iconfont icon-tupian"></span>
          3
        </div>
      </div>
    </div>
    <common-gallary :imgs="imgs"
                    v-show="showGallary"
                    @close="handleGallaryClose"></common-gallary>
  </div>
</template>

<script>
import CommonGallary from 'common/gallary/Gallary'
export default {
  name: 'DetailBanner',
  data () {
    return {
      showGallary: false,
      imgs: ['http://img1.qunarzz.com/sight/p0/1809/86/86d76042cc6581f9a3.img.jpg_r_800x800_429f4dca.jpg',
        'http://img1.qunarzz.com/sight/p0/1809/fa/faa841bf8c7fe255a3.img.jpg_r_800x800_9b3b1c63.jpg',
        'http://img1.qunarzz.com/sight/p0/1809/c9/c9ab2722d2990967a3.img.jpg_r_800x800_2ab18a45.jpg']
    }
  },
  methods: {
    handleBannerClick () {
      this.showGallary = true
    },
    handleGallaryClose () {
      this.showGallary = false
    }
  },
  components: {
    CommonGallary: CommonGallary
  }
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
