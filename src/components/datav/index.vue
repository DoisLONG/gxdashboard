<template>
  <div :id="isMobile? 'data-view2':'data-view'">
    <dv-full-screen-container v-if="!isMobile">
      <div class="main-header">
        <div class="mh-middle">机电设备电子档案</div>
        <div class="mh-right">
          <dv-border-box-2
            style="width: 120px; height: 50px; line-height: 50px; text-align:center;margin-left:200px;"
          >
            综合管理台
          </dv-border-box-2>
        </div>
      </div>

      <dv-border-box-1 class="main-container">
        <dv-border-box-3 class="left-chart-container">

          <Left-Chart-1 />
          <Left-Chart-2 />
          <Left-Chart-3 />

        </dv-border-box-3>

        <div class="right-main-container">
          <div class="rmc-top-container">
            <dv-border-box-3 class="rmctc-left-container">

              <Center-Cmp />

            </dv-border-box-3>

            <div class="rmctc-right-container">
              <dv-border-box-3 class="rmctc-chart-1">

                <Right-Chart-1 />

              </dv-border-box-3>

              <dv-border-box-4 class="rmctc-chart-2" :reverse="true">

                <Right-Chart-2 />

              </dv-border-box-4>
            </div>
          </div>

          <dv-border-box-4 class="rmc-bottom-container">

            <Bottom-Charts />

          </dv-border-box-4>
        </div>
      </dv-border-box-1>

    </dv-full-screen-container>

     <div v-if="isMobile" id="dv-full-screen-container2">
      <div class="main-header">
        <div class="mh-middle">机电设备电子档案</div>
      </div>


        <dv-border-box-3 class="left-chart-container">

          <Left-Chart-1 />
          <Left-Chart-2 />
          <Left-Chart-3 />

        </dv-border-box-3>

        <div class="right-main-container">
          <div class="rmc-top-container">
            <dv-border-box-3 class="rmctc-left-container">

              <Center-Cmp :is-mobile="isMobile"/>

            </dv-border-box-3>

            <div class="rmctc-right-container">
              <dv-border-box-3 class="rmctc-chart-1">

                <Right-Chart-1 />

              </dv-border-box-3>

              <dv-border-box-4 class="rmctc-chart-2" :reverse="true">

                <Right-Chart-2 />

              </dv-border-box-4>
            </div>
          </div>

          <dv-border-box-4 class="rmc-bottom-container">

            <Bottom-Charts :is-mobile="isMobile" />

          </dv-border-box-4>
        </div>

    </div>
  </div>
</template>

<script>
import LeftChart1 from './LeftChart1'
import LeftChart2 from './LeftChart2'
import LeftChart3 from './LeftChart3'

import CenterCmp from './CenterCmp'

import RightChart1 from './RightChart1'
import RightChart2 from './RightChart2'

import BottomCharts from './BottomCharts'

export default {
  name: 'DataView',
  components: {
    LeftChart1,
    LeftChart2,
    LeftChart3,
    CenterCmp,
    RightChart1,
    RightChart2,
    BottomCharts
  },
  data () {
    return {
      isMobile:false
    }
  },
  // vue的生命周期函数（自带的，和created同级），它的生效时间在created之前
  mounted() {
    // 监听函数，对屏幕大小进行监听，屏幕有变化的时候，就触发checkIfMobile函数
    this.checkIfMobile()
    // html自带的函数，作用是增加对屏幕大小的监听，resize表明对屏幕的大小进行监听，后面的callback，是屏幕
    // 大小变化的时候被触发的函数。在这里使用之前写好的checkIfMobile,
    window.addEventListener("resize", this.checkIfMobile)
  },
  // 在关闭页面或者离开页面之前，去除监听器，释放浏览器的性能
  beforeDestroy() {
    window.removeEventListener("resize", this.checkIfMobile)
  },
  methods: {
    checkIfMobile() {
      this.isMobile = window.innerWidth <= 768
    }
  }
}
</script>

<style lang="less">
#data-view {
  width: 100%;
  height: 100%;
  background-color: #030409;
  color: #fff;

  #dv-full-screen-container {
    background-image: url('./img/bg.png');
    background-size: 100% 100%;
    box-shadow: 0 0 3px blue;
    display: flex;
    flex-direction: column;
  }

  .main-header {
    height: 80px;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;

    .mh-left {
      font-size: 20px;
      color: rgb(1,134,187);

      a:visited {
        color: rgb(1,134,187);
      }
    }

    .mh-middle {
      font-size: 30px;
    }

    .mh-left, .mh-right {
      width: 450px;
    }
  }

  .main-container {
    height: calc(~"100% - 80px");

    .border-box-content {
      padding: 20px;
      box-sizing: border-box;
      display: flex;
    }
  }

  .left-chart-container {
    width: 22%;
    padding: 10px;
    box-sizing: border-box;

    .border-box-content {
      flex-direction: column;
    }
  }

  .right-main-container {
    width: 78%;
    padding-left: 5px;
    box-sizing: border-box;
  }

  .rmc-top-container {
    height: 65%;
    display: flex;
  }

  .rmctc-left-container {
    width: 65%;
  }

  .rmctc-right-container {
    width: 35%;
  }

  .rmc-bottom-container {
    height: 35%;
  }

  .rmctc-chart-1, .rmctc-chart-2 {
    height: 50%;
  }
}
@media(max-width: 480px){
  #data-view2 {
  width: 100%;
  height: auto;
  background-color: #030409;
  color: #fff;
  #dv-full-screen-container2 {
      width: 100%;
      height: auto;
      background-image: url("./img/bg.png");
      background-size: 100% 100%;
      box-shadow: 0 0 3px blue;
      background-position: center center;
      background-repeat: no-repeat;
      background-attachment: fixed;
      background-size: cover;
  }

  .main-header {
    height: 80px;
    line-height: 80px;
    // justify-content: space-between;
    // align-items: flex-end;

    .mh-left {
      font-size: 20px;
      color: rgb(1,134,187);

      a:visited {
        color: rgb(1,134,187);
      }
    }

    .mh-middle {
      font-size: 30px;
    }

    .mh-left, .mh-right {
      width: 450px;
    }
  }


  .left-chart-container {
    width: 95% !important;
    height: 95vh;
    margin-left: 2%;
    padding: 10px;
    // box-sizing: border-box;

    .border-box-content {
      flex-direction: column;
    }
  }

  .right-main-container {
    width: 95%;
    padding-left: 5px;
    // box-sizing: border-box;
  }

  .rmc-top-container {
    width: 100%;
    height: 65%;
    // display: flex;
  }

  .rmctc-left-container {
    width: 100% !important;
    height: 70vh;
  }

  .rmctc-right-container {
    width: 100% !important;
    height: 70vh;
  }

  .rmc-bottom-container {
    height: 125vh;
  }

  .rmctc-chart-1, .rmctc-chart-2 {
    height: 50%;
  }
}
}
</style>
