---
title: slide
pageClass: custom-page-class
---
<clientOnly>
<demo name="slide" detail="拖动更改每个区域的大小">
<zslide></zslide>
<highlight-code slot="code" lang="vue" class="code">
&ltzslide :slideList="slideList" @handleSlide="slide">&lt/zslide>
&ltscript&gt 
export default {
    data() {
        slideList: [
        { color: '#67C23A', level: 'A', min: 0, max: 10 },
        { color: '#6354e9', level: 'B', min: 10, max: 20 },
        { color: '#38bedf', level: 'C', min: 20, max: 100 }
      ],
    },
    methods: {
      slide(v) {
        console.log('slide', v)
      }
    }
}
&lt/script&gt
</highlight-code>
</demo>
<params :list="list"></params>
</clientOnly> 

<script>
export default {
    data() {
        return {
            list: [
                {params: 'slideList', detail: '滑动条参数', type: 'Array', choose: '-', default: '[]'},
            ]
        }
    }
}
</script>

<style>

</style>