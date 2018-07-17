<template>
  <div class="container" @click="handleGallaryClick">
    <div class="wrapper">
      <swiper :options="swiperOption">
        <!-- slides -->
        <swiper-slide v-for="(item,key) of gallaryImgs" :key="key">
          <img class="swiper-img" :src="item">
        </swiper-slide>
        <!-- Optional controls -->
        <div class="swiper-pagination" slot="pagination"></div>
      </swiper>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Gallery',
  props: {
    gallaryImgs: {
      type: Array
      // default () {
      //   return ['http://img1.qunarzz.com/sight/p0/201404/23/04b92c99462687fa1ba45c1b5ba4ad77.jpg_800x800_70debc93.jpg',
      //     'http://img1.qunarzz.com/sight/p0/1709/76/7691528bc7d7ad3ca3.img.png_800x800_9ef05ee7.png']
      // }
    }
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        paginationType: 'fraction',
        observeParents: true,
        observer: true

      }
    }
  },
  methods: {
    handleGallaryClick () {
      this.$emit('close')
    }
  }

}
</script>

<style lang="stylus" scoped>

  .container >>> .swiper-container
    overflow inherit

  .container
    position fixed
    z-index: 5
    left: 0
    right 0
    top: 0
    bottom 0
    display: flex
    flex-direction column
    justify-content center
    background-color #000
    .wrapper
      width 100%
      height 100vw
      .swiper-img
        width: 100%
      .swiper-pagination
        color: #ffffff
        bottom -1rem
</style>
