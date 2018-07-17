<template>
  <ul :class="{list:true,blackGround:isTouching}"  ref="list"
      @touchstart="handleUlTouchstart"
      @touchend="handleUlTouchend"
      @touchmove="handleUlTouchmove">
    <li class="item" v-for="item of letters"
        @click="handleLiClick"
        :ref="item"
        :key="item">{{item}}
    </li>
  </ul>
</template>

<script>

function getAbsolutePosition (reference, target) {
  // 因为我们会将目标元素的边框纳入递归公式中，这里先减去对应的值
  let result = {
    left: -target.clientLeft,
    top: -target.clientTop
  }
  let node = target
  while (node !== reference && node !== document) {
    result.left = result.left + node.offsetLeft + node.clientLeft
    result.top = result.top + node.offsetTop + node.clientTop
    node = node.parentNode
  }
  if (isNaN(reference.scrollLeft)) {
    result.right = document.documentElement.scrollWidth - result.left
    result.bottom = document.documentElement.scrollHeight - result.top
  } else {
    result.right = reference.scrollWidth - result.left
    result.bottom = reference.scrollHeight - result.top
  }
  return result
}

export default {
  name: 'Alhpabet',
  data () {
    return {
      touchState: false,
      startY: 0,
      isTouching: false
    }
  },
  props: {
    cities: Object
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  updated () {
    this.startY = getAbsolutePosition(document, this.$refs['A'][0]).top
  },
  methods: {
    handleUlTouchstart (e) {
      this.isTouching = true
    },
    handleUlTouchend (e) {
      this.isTouching = false
    },
    handleUlTouchmove (e) {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      this.timer = setTimeout(() => {
        let index = Math.floor((e.touches[0].clientY - this.startY) / 20)
        if (index >= 0 && index < 22) {
          this.$emit('changeLetter', this.letters[index])
        }
      }, 16)
    },
    handleLiClick (e) {
      this.$emit('changeLetter', e.target.innerText)
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import "~@/assets/style/variables.styl"
  .list
    position absolute
    top: 1.58rem
    right: 0
    display: flex
    flex-direction: column
    justify-content: center
    bottom: 0
    width: .4rem
    .item
      line-height: .4rem
      text-align: center
      color: $themColor
  .blackGround
    background: rgba(0, 0, 0, 0.1)

</style>
