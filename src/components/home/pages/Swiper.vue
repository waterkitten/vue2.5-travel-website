<template>
  <swiper ref="mySwiper" :options="swiperOptions">
    <swiper-slide>
      <img
        src="http://5b0988e595225.cdn.sohucs.com/images/20180412/eb70ca29a8e54a2988cb7e4d6f87bc12.png"
      />
    </swiper-slide>
    <swiper-slide>
      <img
        src="http://5b0988e595225.cdn.sohucs.com/images/20180412/e84e8bff26324d5b89a6cec930df8cd9.png"
    /></swiper-slide>
    <swiper-slide>
      <img
        src="https://i.pximg.net/img-master/img/2016/02/02/02/36/26/55040756_p0_master1200.jpg"
    /></swiper-slide>
    <swiper-slide>
      <img
        src="https://i.pximg.net/img-master/img/2017/06/01/08/51/34/63166871_p0_master1200.jpg"
    /></swiper-slide>
    <swiper-slide>
      <img
        src="https://i.pximg.net/img-master/img/2016/01/11/07/24/37/54657215_p0_master1200.jpg"
    /></swiper-slide>
    <div class="swiper-pagination" slot="pagination"></div>
  </swiper>
</template>

<script>
export default {
  name: "HomeSwiper",
  data() {
    return {
      swiperOptions: {}
    };
  }
};
</script>
<style lang="stylus" scoped></style>
