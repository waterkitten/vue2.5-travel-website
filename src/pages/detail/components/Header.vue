<template>
  <div>
    <router-link tag="div"
                 to="/"
                 class="header-abs"
                 v-show="showAbs">

      <div class="iconfont icon-fanhui"></div>
    </router-link>
    <div class="header-fixed"
         v-show="!showAbs"
         :style="opacityStyle">
      <router-link to="/">
        <div class="iconfont icon-fanhui fix-fanhui"></div>
      </router-link>
      旅游详情
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 65) {
        let opacity = top / 145
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = { opacity: opacity }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
      // console.log(document.documentElement.scrollTop)
    }

  },
  activated () {
    window.addEventListener('scroll', this.handleScroll)
  },
  deactivated () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.header
  display flex
  line-height $headerHeight
  background $bgColor
  color #fff
  .header-left
    width 0.64rem
    float left
    color #fff
    .icon-fanhui
      text-align center
      font-size 0.4rem
.header-abs
  position absolute
  left 0.2rem
  top 0.2rem
  width 0.8rem
  height 0.8rem
  line-height 0.8rem
  border-radius 0.4rem
  text-align center
  background rgba(0, 0, 0, 0.8)
  color #fff
  .abs-fanhui
    font-size 0.4rem
    color #fff
.header-fixed
  position fixed
  top 0
  left 0
  right 0
  height $headerHeight
  line-height $headerHeight
  text-align center
  color #fff
  background $bgColor
  font-size 0.32rem
  .fix-fanhui
    position absolute
    top 0
    left 0
    width 0.64rem
    text-align center
    font-size 0.4rem
    color #fff
</style>
