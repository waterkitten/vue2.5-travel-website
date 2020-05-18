<template>
  <div class="header">
    <div class="header-left">
      <div class="iconfont back-icon">
        &#xe624;
      </div>
    </div>
    <div class="header-search">
      <span class="iconfont arrow-icon">
        &#xe632;
      </span>
      输入城市/景点/游玩主题
    </div>
    <router-link to='/city'>
      <div class="header-right">
        北京<span class="iconfont">
          &#xe65c;
        </span>
      </div>
    </router-link>
  </div>
</template>
<script>
import { mapState } from 'vuex'
export default {
  name: 'HomeHeader',
  computed: {
    ...mapState(['city'])
  }
}
</script>
<style scoped lang='stylus'>/* 局部 */
@import '~css/var.stylus'
.header
  width 100%
  line-height 0.88rem
  background $bgColor
  font-size 0.36rem
  color $textColor
  display flex
  .back-icon
    text-align center
    font-size 0.4rem
.header-left
  width 0.4rem
  padding 0 0.2rem
  text-align center
  font-weight bold
.header-search
  flex 1
  background #fff
  font-size 0.28rem
  line-height 0.6rem
  height 0.6rem
  margin 0.14rem 0
  border-radius 0.09rem
  color #e4e7ea
  padding-left 0.2rem
.header-right
  font-size 0.28rem
  padding 0 0.2rem
.arrow-iconfon
  margin-left -0.04rem
  font-size 0.24rem
</style>