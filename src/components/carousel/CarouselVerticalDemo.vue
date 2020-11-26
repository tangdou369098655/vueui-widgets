<template>
<div id="webgl03_index">
  <!-- 测试版本demo3纵向缓慢滚动 -->
  <dv-full-screen-container class="bg">
    <!-- 如果正在加载，就会盖住展示内容 -->
    <dv-loading v-if="loading">Loading...</dv-loading>
    <!-- 主界面 -->
    <div v-else class="host-body">
      <div style="height: 6.296%;"></div>
      <!-- 下部分 -->
      <div class="mybottom">
        <!-- 下部分模块--右边 -->
        <div class="mybottom_right">
          <!-- 改为轮播图类型 -->
          <div>
            <dv-loading v-if="smallLoading" style="height:900px">Loading...</dv-loading>
            <CarouselOne autoplay v-model="value2" loop :autoplaySpeed="80000" :height="918" :len="myCarouselArr.length">
              <template slot="one">
                <CarouselItem v-for="(myItem, i) of myCarouselArr" :key="i+1">
                  <div class="right_bottom">
                    <SmallChart v-for="(item,index) in myItem" :key="item.domId" :data="item" :ref="'smallChart'+i+index"></SmallChart>
                  </div>
                </CarouselItem>
              </template>
              <template slot="two">
                <CarouselItem v-for="(myItem, i) of myCarouselArr" :key="i+12">
                  <div class="right_bottom">
                    <SmallChart v-for="(item,index) in myItem" :key="item.domId" :data="item" :ref="'smallChart'+i+index"></SmallChart>
                  </div>
                </CarouselItem>
              </template>
            </CarouselOne>
          </div>
          <!-- 改为轮播图类型 -->
        </div>
        <!-- 下部分模块--右边 -->
      </div>
      <!-- 下部分 -->
      <!-- 测试按钮 -->
      <!-- <div>
        <button @click="changeShow">删除</button>
      </div> -->
      <!-- 测试按钮 -->
    </div>
    <!-- 主界面 -->
  </dv-full-screen-container>
</div>
</template>

<script>
import CarouselOne from '../co-assets/components/carousel/CarouselOne'
import CarouselItem from '../co-assets/components/carousel/CarouselItem'
import SmallChart from './co-components/SmallChart'
import mockJs from './co-assets/js/mock.js'
var timer = {
  first: null,
  second: null,
  third: null,
  fourth: null
}
export default {
  name: 'WhiteTest2',
  components: {
    SmallChart,
    CarouselOne,
    CarouselItem
  },
  data() {
    return {
      value2: 0,
      show: false,
      smallLoading: true,
      smallListData: [],
      myCarouselArr: [],
      currentNum: 0,
      currentString: '0',
      chartArr: [], // 圖表列表數據，具體格式可以參考一下子組件
      loading: false // 如果正在加载，就会盖住展示内容
    }
  },
  created() {
    this.getData()
    // console.log('调用了生命周期-----主页面')
  },
  mounted() {
    this.chartArr = mockJs.chartArr
    this.getData()
  },
  methods: {
    changeShow() {
      this.show = !this.show
    },
    clearData() {
      timer.first = null
      timer.second = null
      timer.third = null
      timer.fourth = null
      // console.log('调用了刷新页面-----clearData---------父组件WEBGL03')
    },
    async getData() {
      this.dealData()
    },
    dealData() {
      this.myCarouselArr = mockJs.chartArr1 
      this.myCarouselArr.forEach((_, i) => {
        _.forEach((item, index) => {
          this.$refs &&
            this.$refs['smallChart' + i + index] &&
            this.$refs['smallChart' + i + index][0] &&
            this.$refs['smallChart' + i + index][0].reFresh()
        })
      })
      // console.log('this.myCarouselArr')
      // console.log(JSON.stringify(this.myCarouselArr))
      this.smallLoading = false
      // 处理图表数据
    }
  },
  beforeDestroy() {
    clearInterval(timer.first)
    this.clearData()
  }
}
</script>

<style lang="less" scoped>
#webgl03_index {
  color: white;
  background: #060d27;
  width: 100%;
  height: 100vh;

  .bg {
    padding: 0;
  }

  .flex_space {
    display: flex;
    justify-content: space-between;
  }

  .host-body {
    width: 100%;
    height: 100%;

    // 顶部
    // 下部分
    .mybottom {
      padding: 1.56% 1.56%;
      display: flex;
      background: #060d27;
      height: 93.704%;
      overflow: hidden;
      justify-content: space-between;

      // 下部分模块--右边
      .mybottom_right {
        width: 72%;

        /deep/.el-carousel__container {
          height: 918px;
        }

        .right_bottom {
          margin-top: 70px;
          // margin-top: 10px;
          display: flex;
          flex-wrap: wrap;
          justify-content: space-between;
        }
      }

      // 下部分模块--右边
    }

    // 通用資料
    .little_box {
      width: 0.1rem;
      height: 0.2rem;
      background-color: #49e0ff;
    }

  }

  .demo-carousel {
    height: 200px;
    line-height: 200px;
    text-align: center;
    color: #fff;
    font-size: 20px;
    background: #506b9e;
  }
}
</style>
