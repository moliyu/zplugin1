<template>
  <div id="app">
    <zbutton normal>my name is</zbutton>
    <zswitch :toggle="toggle" @click.native="toggle=!toggle" open="red" close="yellow" w="60" h="20" style="margin-top:20px"></zswitch>
    <!-- <ztable ref="jj" @chooseList='getList' center :border='true' :dataList="list" :header="header" style="margin-top:20px" :per="[4,1,3]">
        <template v-slot:数据="row">
            <div>{{row.header.data}}</div>
        </template>
        <template v-slot:2=row>
            <div @click="select(row.body.data)">{{row.body.data}}</div>
        </template>
        <template v-slot:0="row">
          <div v-if="row.body.i==1" @click="cl(row)">dog</div>
        </template>
    </ztable>-->
    <zprogress :per="per" bg="red" perbg="green" :play="true" style="width: 200px" h="30"></zprogress>
    <ztable
      :header="header"
      :dataList="list"
      style="marginTop: 20px;"
      :trStyle="{border: '1px solid'}"
      center
      :cellStyle="{color: 'green'}"
      :select="toggle"
      :widthList="['30%','','10%']"
      @chooseList="chooseList"
    >
      <template v-slot:姓名="row">{{row.header.data.name}}</template>
      <template v-slot:name="row">{{row.body.data}}</template>
      <div slot="表头">1234</div>
    </ztable>
    <zcalenda :date="{year: 2020, month: 6, day: 20}" style="width: 300px;border: 1px solid" :range="true" @select="select"></zcalenda>
    <!-- <div id="wave" class="wave" ref="wave"></div>
    <div id="timeline"></div>
    <div class="play">
      <zbutton @click.native="playaudio">播放</zbutton>
      <zbutton @click.native="pauseaudio">暂停</zbutton>
      <zbutton @click.native="stopaudio">停止</zbutton> 
      <zbutton @click.native="deleteregion">删除</zbutton> 
    </div>-->
    <zbutton @click.native="show1=!show1">yi</zbutton>
    <zcollapse>
      <div v-if="show1" style="padding: 10px; background: red; padding: 20px">
        <div>dog</div>
        <div>dog</div>
        <div>dog</div>
        <div>dog</div>
      </div>
    </zcollapse>
    <div>
      <zbutton @click.native="show2=!show2">dianji</zbutton>
      <zcollapse>
        <div v-if="show2" style="background: yellow;">fjoiwjfo</div>
      </zcollapse>
    </div>
    <zslide :slideList="evalList"></zslide>
  </div>
</template>

<script>
import zbutton from './plugins/zbutton/zbutton'
import zswitch from '@/plugins/zswitch/zswitch'
import zprogress from '@/plugins/zprogress/zprogress'
import ztable from '@/plugins/ztable/ztable'
import { getdata } from "@/plugins/ztable/test"
import zcalenda from './plugins/zcalenda/zcalenda'
import { pmctowav } from './utils'
import axios from 'axios'
import zcollapse from './plugins/zcollapse/zcollapse.js'
import zslide from './plugins/zslide/zslide'
// import zcollapse from './utils' 
export default {
  name: 'app',
  components: {
    zbutton,
    zswitch,
    zprogress,
    ztable,
    zcalenda,
    zcollapse,
    zslide
  },
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      show1: false,

      show2: false,
      cList: [
        { theme: '主题', content: '内容' },
        { theme: '主题1', content: '内容1' },
      ],
      toggle: true,
      per: 0,
      header: [
        { prop: 'name', name: '姓名', width: '100px' },
        { prop: 'value', name: '数据' },
        { prop: 'cat', name: '表头' }
      ],
      evalList: [
        { color: '#67C23A', level: 'A', min: 0, max: 10 },
        { color: '#6354e9', level: 'B', min: 10, max: 20 },
        { color: '#38bedf', level: 'C', min: 20, max: 100 }
      ],
      list: [
        // { value: 'a的数据',name: 'a', cat:false},
        // { value: 'b的数据',name: 'b', cat: false}
      ],
      ppp: 'jjjj',
      file: 'http://localhost:8000/001.wav',
      waveSurfer: null,
      region: null,
      regionsList: []
    }
  },
  created() {
    getdata().then(data => {
      // console.log('iiii', data)
      this.list = data
    })
  },
  methods: {
    getList(val) {
      // console.log(val,8888)
    },
    select(val) {
      console.log(val)
      val.cat = !val.cat
      // row.body.cat = !row.body.cat
    },
    tes() {
      this.ppp = "qqq"
    },
    playaudio() {
      this.waveSurfer.play()
      // this.waveSurfer.zoom(100)
    },
    pauseaudio() {
      this.waveSurfer.pause()
    },
    stopaudio() {
      this.waveSurfer.stop()
    },
    deleteregion() {
      this.region.remove()
    },
    select(val) {
      console.log('sss', val)
    },
    chooseList(v) {
      console.log('iii', v)
    }
  }
}
</script>

<style lang="scss">
  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-left: 10px;
  }

  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  h1,
  h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }

  .test {
    color: pink;
  }
</style>
