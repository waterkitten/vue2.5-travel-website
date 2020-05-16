<template>
  <div>
    <div class="title">热门推荐</div>
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
          imgUrl: 'http://img1.qunarzz.com/sight/p0/201406/04/4f597aad25208a233999238c65af9b06.jpg_200x200_d1ea2bd2.jpg',
          title: '南京珍珠泉水上世界',
          desc: '高品质天然泉水水上乐园'
        }, {
          id: '0002',
          imgUrl: 'http://img1.qunarzz.com/sight/p0/1805/9b/9b3cbcf2624bf8cea3.img.jpg_200x200_075bc9ef.jpg',
          title: '弘阳未来世界主题乐园',
          desc: '带你快乐一夏天'
        }, {
          id: '0003',
          imgUrl: 'http://img1.qunarzz.com/sight/p0/1411/b3/1415e635014967c75a3d955ae256a628.water.jpg_200x200_54ee590f.jpg',
          title: '南京汤山一号温泉',
          desc: '南京本月收藏Top5╰(￣▽￣)╭'
        }, {
          id: '0004',
          imgUrl: 'http://img1.qunarzz.com/sight/p0/1703/58/589f52a494f307d3a3.water.jpg_200x200_71b77fd4.jpg',
          title: '巴布洛生态谷',
          desc: '健康生活之门为你打开'
        }, {
          id: '0005',
          imgUrl: 'http://img1.qunarzz.com/sight/p0/1504/15/1530936526074f62.water.jpg_200x200_fb55ee43.jpg',
          title: '六朝博物馆',
          desc: '研究六朝历史文化的专题博物馆'
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
  background #90EE90
  text-align center
  box-shadow 0 0 20px 13px black
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
    background #90EE90
    padding 0 1rem
    border-radius 0.06rem
    color #fff
    font-size 0.5rem
    text-shadow 4px 3px 16x
</style>