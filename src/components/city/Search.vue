<template>
  <div class="search">
    <input class="search-input"
           type="text"
           placeholder="输入城市名或拼音">
  </div>
</template>

<script>
export default {
  name: 'CitySearch'
}
</script>

<style lang="stylus" scoped>
@import '~css/var.stylus'
.search
  height 0.88rem
  padding 0 0.1rem
  background #FFA500
  .search-input
    box-sizing border-box
    width 100%
    height 0.99rem
    padding 0 0.1rem
    line-height 0.88rem
    text-align center
    border-radius 0.06rem
    color #666
</style>