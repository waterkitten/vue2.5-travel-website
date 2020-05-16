<template>
  <div>
    <HomeHeader />
    <home-swiper></home-swiper>
    <home-icons></home-icons>
    <home-recommend></home-recommend>
    <home-weekend></home-weekend>

  </div>
</template>
<script>
import HomeHeader from "./pages/Header";
import HomeSwiper from "./pages/Swiper";
import HomeIcons from "./pages/Icons"
import HomeRecommend from './pages/Recommend'
import HomeWeekend from './pages/Homeweekend'
export default {
  components: {
    HomeHeader,
    HomeSwiper,
    HomeIcons,
    HomeRecommend,
    HomeWeekend

  }
};
</script>
<style></style>
