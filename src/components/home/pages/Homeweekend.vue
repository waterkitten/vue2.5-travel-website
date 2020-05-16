<template>
  <div>
    <div class="title">周末去哪儿</div>
    <ul>
      <li class="item border-bottom"
          v-for="item of list"
          :key='item.id'>

        <img class="item-img"
             :src="item.imgUrl"
             alt="">

        <div class="item-info">
          <p class="item-title">{{item.title}}</p>
          <p class="item-desc border-bottom">{{item.desc}}</p>
          <button class="item-button">查看详情</button>
        </div>

      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HomeRecommend',
  data () {
    return {
      list: [
        {
          id: '0001',
          imgUrl: 'http://img1.qunarzz.com/sight/source/1505/f3/d51669250308cc.jpg_r_640x214_7a127cd0.jpg',
          title: '秦淮金粉里的南京',
          desc: '六朝金粉，处处诉说着南京的历史'
        }, {
          id: '0002',
          imgUrl: 'http://img1.qunarzz.com/sight/source/1505/f1/ae9d4299b8aaea.jpg_r_640x214_0c555905.jpg',
          title: '南京必游TOP10',
          desc: '看尽王侯将相荣辱成败，六朝金粉潮起潮落'
        }, {
          id: '0003',
          imgUrl: 'http://img1.qunarzz.com/sight/source/1505/e1/cdbf56d837da59.jpg_r_640x214_105fc3f2.jpg',
          title: '民国情怀国共风华',
          desc: '找到你心中想要的那个民国时期的南京'
        }, {
          id: '0004',
          imgUrl: 'http://img1.qunarzz.com/sight/source/1505/ed/8bce72632c9136.jpg_r_640x214_221c04c6.jpg',
          title: '孩子的游玩地',
          desc: '让小朋友们欢脱起来'
        }
      ]
    }
  }
}
</script>

<style scoped lang='stylus'>/* 局部 */
@import '~css/var.stylus'
.title
  line-height 1.1rem
  background #FFD700
  text-align center
.item
  display flex
  overflow hidden
  height 3rem
  .item-img
    height 3rem
    width 4rem
    padding 0.1rem
.item-info
  flex 1
  padding 0.1rem
  min-width 0
  box-shadow 0 0 20px 20px black
  .item-title
    line-height 0.54rem
    font-size 0.8rem
    ellipsis()
  .item-desc
    position relative
    line-height 0.4rem
    color #ccc
    width 100%
    ellipsis()
  .item-button
    line-height 0.77rem
    margin-top 1rem
    background #ff9300
    padding 0 1rem
    border-radius 0.06rem
    color #fff
    font-size 0.5rem
    text-shadow 4px 3px 16x
</style>