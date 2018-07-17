<template>
  <div>
    <div class="banner" @click="handleBannerClick">
      <img class="banner-img" :src='bannerImg'/>
      <div class="banner-info">
        <div class="banner-title">{{sightName}}</div>
        <div class="banner-number"><span class="iconfont banner-icon">&#xe632;</span>39</div>
      </div>
    </div>
    <fade-animation>
      <common-gallery
        v-show="showGallery"
        @close="handleGalleryClose"
        :gallaryImgs="gallaryImgs"
      ></common-gallery>
    </fade-animation>
  </div>
</template>

<script>
import CommonGallery from 'common/gallery'
import FadeAnimation from 'common/fade/fadeAnimation'
export default {
  name: 'index',
  components: {
    CommonGallery, FadeAnimation
  },
  props: {
    sightName: String,
    bannerImg: String,
    gallaryImgs: Array
  },
  data () {
    return {
      showGallery: false
    }
  },
  methods: {
    handleBannerClick () {
      this.showGallery = true
    },
    handleGalleryClose () {
      this.showGallery = false
    }
  }
}
</script>

<style lang="stylus" scoped>
  .banner
    position relative
    width: 100%
    height 55vw
    .banner-img
      width 100%
    .banner-info
      position absolute
      left: 0
      right: 0
      bottom 0
      line-height: .6rem
      display flex
      background-image linear-gradient(top,rgba(0,0,0,0),rgba(0,0,0,.8))
      .banner-title
        color: #ffffff
        font-size:.32rem
        flex:1
      .banner-number
        height: .32rem
        line-height: .32rem
        color: #ffffff
        font-size:.24rem
        padding 0 .4rem
        border-radius: .2rem
        background rgba(0,0,0,.8)
        .banner-icon
          font-size:.24rem

</style>
