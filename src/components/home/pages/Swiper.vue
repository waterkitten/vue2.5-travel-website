<template>
  <div class="wrapper">
    <swiper ref="mySwiper"
            class="out-swiper"
            :options="swiperOption">
      <swiper-slide class="image-slide">
        <img class="swiper-image"
             src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1589546257057&di=6efe91cbe826d04a223c6c3e71abd574&imgtype=0&src=http%3A%2F%2Fhbimg.b0.upaiyun.com%2F90f81a4526290e3bb95f6c3d87829325425b689044d80-BVMEee_fw658" />
      </swiper-slide>
      <swiper-slide class="image-slide">
        <img class="swiper-image"
             src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1589546141975&di=cf00016628b881f9c8e995bb2a289b29&imgtype=0&src=http%3A%2F%2Fn.sinaimg.cn%2Fsinacn23%2F33%2Fw500h333%2F20180613%2F7eaf-hcwpcmq5312135.jpg" /></swiper-slide>
      <swiper-slide class="image-slide">
        <img class="swiper-image"
             src="https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3296219714,2452443564&fm=26&gp=0.jpg" /></swiper-slide>
      <swiper-slide class="image-slide">
        <img class="swiper-image"
             src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1589545744494&di=29c46abc4442b75e0448b604487582e4&imgtype=0&src=http%3A%2F%2Fnews.0554.us%2Fuploads%2Fallimg%2F180719%2F05521R644_0.jpg" /></swiper-slide>
      <swiper-slide class="image-slide">
        <img class="swiper-image"
             src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1589546296802&di=bee327d1f8fe5e6aa1a706a24880964e&imgtype=0&src=http%3A%2F%2Fp.qiuxingwang.cn%2Fd%2Ffile%2Finveno%2F2016-07-15%2F0e76df313059fb9f411415ab8cc22958.jpeg" /></swiper-slide>
      <div class="swiper-pagination"
           slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: "HomeSwiper",
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      }
    };
  }
};
</script>
<style lang="stylus" scoped>
.wrapper
  overflow hidden
  padding-bottom 1px
  height 250px
  .out-swiper
    height 250px
  .image-slide
    text-align center
    width 450px
    height 250px
    .swiper-image
      width 60%
      height 100%
      text-align center
</style>
