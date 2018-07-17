<template>
  <div class="icons">
    <swiper :options="swiperOption"  >
      <swiper-slide v-for="(page,index) of pages" :key="index" >
        <div class='icon' v-for="icon of page" :key="icon.id">
          <div class='icon-img'>
            <img class='icon-img-content' :src='icon.imgUrl'/>
          </div>
          <p class="icon-desc">{{icon.desc}}</p>
        </div>
      </swiper-slide>
      <div class="swiper-pagination pagination-postion" slot="pagination"></div>
    </swiper>

  </div>
</template>

<script>
export default {
  name: 'HomeIcons', // 这个天坑啊，不能重名啊
  props: {
    iconList: Array
  },
  computed: {
    pages () {
      const pages = []
      this.iconList.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }

  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        autoplay: false
      }
    }
  }
}
</script>

<style lang="stylus" scoped>

  @import '~styles/variables.styl'
  @import '~styles/mixins.styl'
  /*.icons >>> .swiper-container*/
  /*height: 0*/
  /*padding-bottom: 50%*/
  .icons
    margin-top: .1rem
    height: 3.8rem
    overflow hidden
    .icon
      float: left
      width: 25%
      height 50%
      padding-top 0.06rem
      .icon-img
        .icon-img-content
          width: 1.1rem
          height: 1.1rem
          display: block
          margin: 0 auto
      .icon-desc
        height: .44rem
        line-height: .44rem
        text-align: center
        color: $darkTextColor
        ellipsis()
    .pagination-postion
      position:static
      margin-top 0.06rem

</style>
