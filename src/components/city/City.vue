<template>
  <div>
    <city-header></city-header>
    <search></search>
    <city-list :cities="cities" :hot="hotCities"> </city-list>
  </div>
</template>

<script>
import axios from "axios";
import CityHeader from "./cityheader";
import Search from "./Search";
import CityList from "./citylist";

export default {
  name: "City",
  components: {
    CityHeader,
    Search,
    CityList
  },
  data() {
    return {
      cities: {},
      hotCities: []
    };
  },
  methods: {
    getCityInfo() {
      axios.get("/api/city.json").then(this.handleGetCityInfoSucc);
    },
    handleGetCityInfoSucc(res) {
      res = res.data;
      if (res.ret && res.data) {
        const data = res.data;
        this.cities = data.cities;
        this.hotCities = data.hotCities;
      }
      console.log(res);
    }
  },
  mounted() {
    this.getCityInfo();
  }
};
</script>

<style>
* {
  font-family: Arial, "Microsoft Yahei", "Helvetica Neue", Helvetica, sans-serif;
}
.w {
  max-width: 13rem; /*移动端650px,并且最好使用max-width*/
  margin: 0 auto;
}
</style>
