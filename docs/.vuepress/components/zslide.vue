<template>
  <div class="zslide">
    <zslide :slideList="slideList" @handleSlide="slide"></zslide>
  </div>
</template>

<script>
import zslide from '../../../src/plugins/zslide'
export default {
  components: {
    zslide
  },
  data() {
    return {
      slideList: [
        { color: '#67C23A', level: 'A', min: 0, max: 10 },
        { color: '#6354e9', level: 'B', min: 10, max: 20 },
        { color: '#38bedf', level: 'C', min: 20, max: 100 }
      ],
    }
  },
  methods: {
    slide(v) {
      console.log('slide', v)
    }
  }
}
</script>

<style>
.zslide {
  padding-bottom: 10px;
}
</style>