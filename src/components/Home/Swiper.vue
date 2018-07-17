<template>
  <div class="wrapper">
    <swiper :options="swiperOption" v-if="isShow">
      <!-- slides -->
      <swiper-slide v-for="item in swiperList" :key="item.id">
        <img class="swiper-img" :src="item.imgUrl">
      </swiper-slide>
      <!-- Optional controls -->
      <div class="swiper-pagination"  slot="pagination"></div>
    </swiper>
  </div>

</template>

<script>
export default {
  name: 'HomeSwiper', // 这个天坑啊，不能重名啊
  props: {
    swiperList: Array
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      }
    }
  },
  computed: {
    isShow () {
      return this.swiperList.length
    }
  }
}
</script>

<style lang="stylus" scoped>
  .wrapper >>> .swiper-pagination-bullet-active
    background: #fff
  .wrapper
    /*overflow: hidden*/
    /*width: 100%*/
    /*height: 0*/
    /*padding-bottom: 31.25%*/
    height 31.25vw
    background: #eee
    .swiper-img
      width: 100%
</style>
