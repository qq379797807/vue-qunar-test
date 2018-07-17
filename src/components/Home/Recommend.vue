<template>
  <div>
    <div class="title">热销推荐</div>
    <ul class="container">
      <router-link tag="li" :to="'/detail/'+item.id"
        class="item border-bottom"
        v-for="item of recommendList"
        :key="item.id"
      >
        <img class="item-img" :src="item.imgUrl" />
        <div class="item-info">
          <p class="item-title">{{item.title}}</p>
          <p class="item-desc">{{item.desc}}</p>
          <button class="item-button">查看详情</button>
        </div>
      </router-link>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Recommend',
  props: {
    recommendList: Array
  },
  data () {
    return {

    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/mixins.styl'
  .title
    title()
  .container
    padding-left :.2rem

  .item
    display:flex
    height: 2rem
    padding .2rem 0
    overflow: hidden
    .item-img
      width: 2rem
    .item-info
      padding-left :0.2rem
      min-width: 0
      .item-title
        line-height: .54rem
        font-size: .32rem
        ellipsis()
      .item-desc
        line-height: .4rem
        color: #ccc
        ellipsis()
      .item-button
        line-height: .44rem
        margin-top: .16rem
        background: #ff9300
        padding: 0 .2rem
        border-radius: .06rem
        color: #fff

  .border-bottom
    border-bottom: solid #eee 1px

</style>
