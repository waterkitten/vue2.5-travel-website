<template>
  <div class="list"
       ref="wrapper">
    <div>
      <div class="area">
        <!-- border-topbottom 1像素边框-->
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">南京</div>
          </div>
        </div>
      </div>
      <div class="area">
        <!-- border-topbottom 1像素边框-->
        <div class="title border-topbottom">热门城市</div>
        <div class="button-list">
          <div class="button-wrapper"
               v-for="item of hot"
               :key="item.id">
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>
      <div class="area"
           v-for="(item,key) of cities"
           :key="key"
           :ref="key">
        <div class="title border-topbottom">{{key}}</div>
        <div class="item-list"
             v-for="innerItem of item"
             :key="innerItem.id">
          <div class="item border-bottom">{{innerItem.name}}</div>
          <!-- 最好加个判断，最后不加 border-bottom <div class="item ">阿拉尔</div> -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
export default {
  name: 'CityList',
  props: {
    hot: Array,
    cities: Object,
    letter: String
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper)
  },
  watch: {
    letter () {
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        // console.log(element) //这是个数组
        this.scroll.scrollToElement(element)
      }
    }
  }
}
</script>
<!-- list -->
<!-- left: 0
    right: 0 -->
<!--   要么
     width: 100%;
    max-width: 650px -->
<style lang="stylus" scoped>
@import '~css/var.stylus'
.border-topbottom
  &:before
    border-color #ccc
  &:after
    border-color #ccc
.border-bottom
  &:before
    border-color #ccc
.list
  overflow hidden
  position absolute
  top 1.58rem
  left 0
  right 0
  bottom 0
  .title
    line-height 0.44rem
    background #eee
    padding-left 0.2rem
    color #666
    font-size 0.22rem
    text-align left
  .button-list
    overflow hidden
    padding 0.1rem 0.6rem 0.1rem 0.1rem
    .button-wrapper
      float left
      width 33.33%
      .button
        margin 0.1rem
        padding 0.1rem 0
        text-align center
        border 0.02rem solid #ccc
        border-radius 0.06rem
        font-size 0.26rem
  .item-list
    .item
      line-height 0.72rem
      padding-left 0.2rem
      text-align left
</style>
