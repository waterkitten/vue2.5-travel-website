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
import HomeIcons from "./pages/Icons";
import HomeRecommend from "./pages/Recommend";
import HomeWeekend from "./pages/Homeweekend";
import axios from "axios";

export default {
  components: {
    name: "Home",
    HomeHeader,
    HomeSwiper,
    HomeIcons,
    HomeRecommend,
    HomeWeekend
  },
  methods: {
    getHomeInfo () {
      axios.get("/api/index.json").then(this.getHomeInfoSucc);
    },
    getHomeInfoSucc (res) {
      console.log(res);
    }
  },
  mounted () {
    this.getHomeInfo();
  }
};
</script>
<style></style>
