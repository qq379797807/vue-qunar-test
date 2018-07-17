<template>
  <div>
    <router-link tag="div" class="header-abs" to="/">
      <div class="iconfont header-abs-back">&#xe624;</div>
    </router-link>
    <div class="header-fixed"
         v-show="showFixed"
         :style="opacityStyle"
    >
      <router-link to="/">
        <div class="iconfont header-fixed-back">&#xe624;</div>
      </router-link>
      城市选择
    </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {
      showFixed: false,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  methods: {
    handleScroll () {
      console.log('this.showfixed')
      let top = document.documentElement.scrollTop
      let opacity = top / 140
      opacity = opacity > 1 ? 1 : opacity
      this.opacityStyle = {
        opacity: opacity
      }
      this.showFixed = !!top
    }
  },
  activated () {
    window.addEventListener('scroll', this.handleScroll)
  },
  deactivated () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/variables.styl'

  .header-abs
    position: absolute
    left: .2rem
    top: .2rem
    width: .8rem
    height: .8rem
    line-height: .8rem
    border-radius: .4rem
    text-align: center
    background: rgba(0, 0, 0, .8)
    .header-abs-back
      color: #fff

  .header-fixed
    z-index: 1
    position: fixed
    top: 0
    left: 0
    right:0
    overflow: hidden
    height: $height
    line-height: $height
    text-align: center
    color: #fff
    background: $themColor
    font-size: .32rem
    .header-fixed-back
      position: absolute
      top: 0
      left: 0
      width: .64rem
      text-align: center
      font-size: .4rem
      color: #fff
</style>
