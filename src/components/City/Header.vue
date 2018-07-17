<template>
  <div class="header">
    <router-link to="/">
      <div class="iconfont header-back">&#xe624;</div>
    </router-link>
      城市选择
  </div>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {city: '北京'}
  }
}
</script>

<style lang="stylus" scoped>
  @import "~@/assets/style/variables.styl"

  .header
    position: relative
    line-height $height
    background-color: $themColor
    color:#fff
    text-align center
    font-size .32rem
    .header-back
      position: absolute
      width: .4rem
      text-align: center
      font-size: .36rem
      line-height: $height
      padding: 0 .2rem
      color:#fff

</style>
