<template>
  <ul class="list">
    <li class="item"
        v-for="(item,key) of cities"
        :ref="item"
        :key="key"
        @click="handleLetterClick">{{key}}</li>
  </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },

  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  methods: {
    handleLetterClick (e) {
      this.$emit("change", e.target.innerText);
    }
  },
  data () {
    return {
      touchStatus: false,
      starY: 0,
      timer: null  //节流
    };
  }

}

</script>

<style lang="stylus" scoped>
@import '~css/var.stylus'
.list
  display flex
  flex-direction column
  justify-content center
  position absolute
  top 1.58rem
  right 0
  bottom 0
  width 0.4rem
  .item
    line-height 0.4rem
    text-align center
    color $bgColor
</style>
