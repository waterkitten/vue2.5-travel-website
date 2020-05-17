<template>
  <div>
    <city-header></city-header>
    <search></search>
    <city-list></city-list>
  </div>
</template>

<script>
import CityHeader from './cityheader'
import Search from './Search';
import CityList from './citylist';
export default {
  name: 'City',
  components: {
    CityHeader,
    Search,
    CityList
  }

}
</script>

<style lang='stylus' scoped></style>