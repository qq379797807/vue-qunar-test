<template>
  <div class="header">
    <div class="iconfont header-left">&#xe624;</div>
    <div class="header-input">
      <span class="iconfont">&#xe632;</span>
      输入城市/景点/游玩主题
    </div>
    <router-link class="header-right" to="/city">
        {{city}}
        <span class="iconfont arrow-icon">&#xe64a;</span>
    </router-link>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  name: 'Header',
  computed: {
    ...mapState(['city'])
  }
}
</script>

<style lang="stylus" scoped>
  @import "~@/assets/style/variables.styl"

  .header
    display: flex
    width 100%
    height: $height
    background-color: $themColor
    .header-left
      width: .4rem
      text-align: center
      font-size: .36rem
      line-height: $height
      padding: 0 .2rem
      color: #fff
    .header-input
      flex: 1
      height: .64rem
      line-height: .64rem
      margin-top: .12rem
      padding: 0 .2rem
      background: #fff
      border-radius: .1rem
      color: #ccc
    .header-right
      min-width: 1.04rem
      height: $height
      line-height: $height
      padding: 0 .2rem
      text-align: center
      color: #fff
      .arrow-icon
        font-size: .24rem

</style>
