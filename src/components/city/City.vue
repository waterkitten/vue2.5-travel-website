<template>
  <div>
    <city-header></city-header>
    <search></search>
    <city-list :cities="cities"
               :hot="hotCities"
               :letter="letter">
    </city-list>
    <city-alphabet :cities="cities"
                   @change='handleLetterChange'></city-alphabet>
  </div>
</template>

<script>
import axios from "axios";
import CityHeader from "./cityheader";
import Search from "./Search";
import CityList from "./citylist";
import Bscroll from "better-scroll";
import CityAlphabet from './Alphabet'
export default {
  name: "City",
  components: {
    CityHeader,
    Search,
    CityList,
    CityAlphabet
  },
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: ''
    };
  },
  methods: {
    getCityInfo () {
      axios.get("/api/city.json").then(this.handleGetCityInfoSucc);
    },
    handleGetCityInfoSucc (res) {
      res = res.data;
      if (res.ret && res.data) {
        const data = res.data;
        this.cities = data.cities;
        this.hotCities = data.hotCities;
      }

    },
    handleLetterChange (letter) {
      this.letter = letter
    }
  },
  mounted () {
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
