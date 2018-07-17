<template>
  <div class="wrapper" ref="wrapper">
    <div>
      <div class="area border-topbottom">
        <div class="title">当前城市</div>
        <ul class="button-list">
          <li class="button-wrapper">
            <div class="button">{{city}}</div>
          </li>
        </ul>
      </div>
      <div class="area border-topbottom">
        <div class="title">热门城市</div>
        <ul class="button-list">
          <li class="button-wrapper"
              v-for="item of hot"
              :key="item.id"
              @click="handleCitySelect(item.name)"
          >
            <div class="button">{{item.name}}</div>
          </li>
        </ul>
      </div>
      <div class="area border-topbottom" v-for="(city,key) of cities" :key="key" :ref="key">
        <div class="title">{{key}}</div>
        <ul class="item-list">
          <li class="item border-bottom"
              v-for="item of city"
              :key="item.id"
              @click="handleCitySelect(item.name)"
          >
            {{item.name}}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
import {mapState, mapMutations} from 'vuex'

export default {
  name: 'List',
  props: {
    cities: Object,
    hot: Array,
    letter: String
  },
  computed: {
    ...mapState(['city'])
  },
  mounted () {
    this.scroll = new BScroll(this.$refs.wrapper)
  },
  methods: {
    ...mapMutations(['changeCity']),
    handleCitySelect (city) {
      this.changeCity(city)
      this.$router.push('/')
    }
  },
  watch: {
    letter () {
      // 省略了判断
      this.scroll.scrollToElement(this.$refs[this.letter][0])
    }
  }
}
</script>

<style lang="stylus" scoped>
  .border-topbottom
    &:before
      border-color: #ccc
    &:after
      border-color: #ccc

  .border-bottom
    &:before
      border-color: #ccc

  .wrapper
    overflow: hidden
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0

    .title
      line-height .44rem
      background-color #eee
      padding-left .2rem

    .button-list
      padding: .1rem .6rem .1rem .1rem
      display flex
      flex-wrap wrap
      .button-wrapper
        width: 33.33%
        .button
          margin .1rem
          padding: .1rem 0
          text-align center
          border: .02rem solid #ccc
          border-radius: .06rem

    .item-list
      .item
        line-height: .76rem
        padding-left: .2rem

</style>
