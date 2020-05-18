<template>
  <div class="icons">
    <swiper>
      <swiper-slide v-for="(page,index) of pages"
                    :key='index'>
        <div class="icon"
             v-for="item of page"
             :Key='item.id'>
          <div class="icon-img">
            <img class="icon-imgcontent"
                 :src="item.imgUrl"
                 alt="">

          </div>
          <p class="icon-desc">{{item.desc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  data () {
    return {
      iconList: [{
        id: '001',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1803/95/f3dd6c383aeb3b02.png',
        desc: '景点门票'
      },
      {
        id: '002',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1803/50/26ffa31b56646402.png',
        desc: '亲子游'
      },
      {
        id: '003',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1804/ff/fdf170ee89594b02.png',
        desc: '厦门必游'
      },
      {
        id: '004',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1803/97/02f5043b51b2102.png',
        desc: '鼓浪屿'
      },
      {
        id: '005',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1804/5a/13ceb38dcf262f02.png',
        desc: '一日游'
      },
      {
        id: '006',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1803/47/c2b659e048b11602.png',
        desc: '主题乐园'
      },
      {
        id: '007',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1803/fa/2548667cb6e902.png',
        desc: '动植物园'
      },
      {
        id: '008',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1803/fa/2548667cb6e902.png',
        desc: '展馆展览'
      },
      {
        id: '009',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1803/89/55083b0f1951f302.png',
        desc: '游船观光'
      },
      {
        id: '010',
        imgUrl: 'http://img1.qunarzz.com/piao/fusion/1803/ab/6f7d6e44963c9302.png',
        desc: '泡温泉'
      }
      ]
    }
  },
  computed: {
    pages () {
      const pages = []
      this.iconList.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
.icons >>>.swiper-container
  height 0
  padding-bottom 50%
.icon
  position relative
  overflow hidden
  float left
  width 25%
  height 0
  padding-bottom 25%
  .icon-img
    top 0
    left 0
    right 0
    bottom 0.44rem
    box-sizing border-box
    padding 0.2rem
      .icon-imgcontent
        height 100%
        display block
        margin 0 auto
      .icon-desc
        overflow hidden
        white-space nowrap
        text-overflow ellipsis
        position absolute
        font-size 25px
        left 0
        right 0
        bottom 0
        height 0.44rem
        text-align center
</style>