<template>
  <div>
    <div class="search">
      <input type="text" class="search-input"
             v-model="keyword"
             placeholder="输入城市名或拼音"/>
    </div>
    <div class="result"
         ref="result"
         v-show="keyword">
      <ul>
        <li v-for="item of list"
            :key="item.id"
            @click="handleCitySelect(item.name)"
            class="item border-bottom"
        >{{item.name}}</li>
        <li class="item border-bottom" v-show="hasNodata">没有找到匹配数据</li>
      </ul>
    </div>
  </div>
</template>

<script>
import {debounce} from 'lodash'
import BScroll from 'better-scroll'
import {mapMutations} from 'vuex'

export default {
  name: 'Search',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: null,
      list: []
    }
  },
  computed: {
    hasNodata () {
      return !this.list.length
    }
  },
  created () {
    this._GetSearchResult = debounce(this.getSearchResult, 100)
  },
  mounted () {
    this.scroll = new BScroll(this.$refs.result)
  },
  watch: {
    keyword () {
      this._GetSearchResult()
    }
  },
  methods: {
    getSearchResult () {
      // 如果不先清空，后续会追加
      this.list = []
      for (let letter in this.cities) {
        this.cities[letter].forEach((city) => {
          if (city.spell.includes(this.keyword) ||
            city.name.includes(this.keyword)) {
            this.list.push(city)
          }
        })
      }
    },
    ...mapMutations(['changeCity']),
    handleCitySelect (city) {
      this.changeCity(city)
      this.$router.push('/')
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import "~@/assets/style/variables.styl"
  .search
    height .72rem
    padding 0 .1rem
    background-color $themColor
    .search-input
      box-sizing: border-box
      width 100%
      padding 0 .1rem
      text-align center
      line-height:.62rem
      border-radius .06rem

  .result
    position absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    z-index 1
    background: #eee
    overflow hidden
    .item
      line-height .76rem
      padding-left: .2rem
      background: #fff
      color: #666

    .border-bottom
      &:before
        border-color: #ccc

</style>
