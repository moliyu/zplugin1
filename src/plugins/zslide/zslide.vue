<template>
  <div class="seteval" ref="content">
    <div class="item" v-for="(item, i) in slideList" :key="i" :style="{width: widthList[i] + item.dx + 'px', ...style(item)}">
      {{item.level}}
      <div class="drag" :style="`height: ${h}`" @mousedown.prevent="down(i, $event)"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    slideList: Array,
    h: {
      default: '40px'
    }
  },
  data() {
    return {
      widthList: [],
      slide: false,
      dx: 0,
      startx: 0,
      moveIndex: -1
    }
  },
  mounted() {
    const len = this.slideList.length
    this.slideList.map((item, i) => {
      if (!item.min && !item.dx && !item.max) {
        this.$set(this.widthList, i, this.fullWidth / len)
        this.$set(item, 'min', 0)
        this.$set(item, 'max', 0)
      } else {
        this.$set(this.widthList, i, this.fullWidth * (item.max - item.min) / 100)
      }
      this.$set(item, 'dx', 0)
    })
  },
  computed: {
    fullWidth() {
      return this.$refs.content.clientWidth
    }
  },
  methods: {
    style(item) {
      return {
        height: this.h,
        background: item.color,
        lineHeight: this.h
      }
    },
    down(i, e) {
      if (i === this.widthList.length - 1) return
      this.slide = true
      this.startx = e.x
      this.moveIndex = i
      document.addEventListener('mousemove', this.move)
      document.addEventListener('mouseup', this.up)
    },
    move(e) {
      let dx = e.x - this.startx
      if (this.widthList[this.moveIndex] + dx <= 0) {
        dx = -this.widthList[this.moveIndex]
      } else if (this.widthList[this.moveIndex + 1] - dx <= 0) {
        dx = this.widthList[this.moveIndex + 1]
      }
      this.slideList[this.moveIndex].dx = dx
      this.slideList[this.moveIndex + 1].dx = -dx
      const list = []
      this.slideList.map((item, i) => {
        if (i === 0) {
          list.push({ min: 0, max: Math.ceil((this.widthList[i] + item.dx) / this.fullWidth * 100) })
        } else if (i === this.slideList.length - 1) {
          list.push({ min: list[i - 1].max, max: 100 })
        } else {
          list.push({ min: list[i - 1].max, max: Math.ceil((this.widthList[i] + item.dx) / this.fullWidth * 100) + list[i - 1].max })
        }
      })
      this.$emit('handleSlide', list)
    },
    up() {
      this.slide = false
      this.slideList.map((item, i) => {
        this.$set(this.widthList, i, this.widthList[i] + item.dx)
        item.dx = 0
        return item
      })
      this.moveIndex = -1
      document.removeEventListener('mousemove', this.move)
      document.removeEventListener('mouseup', this.up)
    }
  }
}
</script>

<style lang="scss" scoped>
.seteval {
  width: 100%;
  .item {
    position: relative;
    display: inline-block;
    text-align: center;
    .drag {
      position: absolute;
      right: -10px;
      width: 20px;
      top: 0;
      cursor: w-resize;
    }
  }
}
</style>
