<template>
  <div class="app-container home">
    <el-row :gutter="10" class="interval">
      <el-col :xs="24" :sm="24" :md="12" :lg="8">
        <div class="item grid-content bg-purple">
          <div class="top_title">
            <div class="left">
              <div class="title_line"></div>
              <span class="text">当月电费</span>
            </div>
          </div>
          <div class="line"></div>
          <div class="bottom">
            <div class="bottom_echart">
              <line-chart :chart-data="lineChartData" />
            </div>
            <div class="bottom_right">
              <div class="title_text">
                <span class="name">电量电费</span>
                <i style="margin-right: 2px">¥</i>
                <span> 19,357.1</span>
              </div>
              <div class="title_text">
                <span class="name">容量电费</span>
                <i style="margin-right: 2px">¥</i>
                <span> 19,357.1</span>
              </div>
              <div class="title_text">
                <span class="name">利率电费</span>
                <i style="margin-right: 2px">¥</i>
                <span> 19,357.1</span>
              </div>
            </div>
          </div>
        </div></el-col
      >
      <el-col :xs="24" :sm="24" :md="12" :lg="8"
        ><div class="item grid-content bg-purple">
          <div class="top_title">
            <div class="left">
              <div class="title_line"></div>
              <span class="text">光储状态</span>
            </div>
            <div class="right">
              <span
                v-for="(item, index) in dataSourceList"
                :key="index"
                @click="searchButton(item.value, 'OpticalStorage')"
                :class="[leftActiveValue === item.value ? 'active' : '']"
              >
                {{ item.label }}
              </span>
            </div>
          </div>
          <div class="line"></div>

          <div class="bottom">
            <div class="bottom_item">
              <div class="data_line">
                <div class="photovoltaic">1348</div>
                <div class="unit">(kWh)</div>
              </div>
              <div class="title">光伏发电量</div>
            </div>
            <div class="bottom_item">
              <div class="data_line">
                <div class="discharge">1348</div>
                <div class="unit">(kWh)</div>
              </div>
              <div class="title">储能放电量</div>
            </div>
            <div class="bottom_item">
              <div class="data_lines">
                <div class="cost">1348</div>
                <div class="unit">(kWh)</div>
              </div>
              <div class="title">储能度电成本</div>
            </div>
            <div class="bottom_item">
              <el-progress type="circle" :percentage="percentage"></el-progress>
              <div class="last_title">消纳率</div>
            </div>
          </div>
        </div></el-col
      >
      <el-col :xs="24" :sm="24" :md="12" :lg="8"
        ><div class="item grid-content bg-purple">
          <div class="top_title">
            <div class="left">
              <div class="title_line"></div>
              <span class="text">收益分析</span>
            </div>
            <div class="right">
              <span
                v-for="(item, index) in dataSourceList"
                :key="index"
                @click="searchButton(item.value, 'income')"
                :class="[activeValue === item.value ? 'active' : '']"
              >
                {{ item.label }}
              </span>
            </div>
          </div>
          <div class="line"></div>

          <div class="bottom">
            <div class="data_line">
              <div class="discharge">1348</div>
              <div class="unit">(kWh)</div>
            </div>
          </div>
        </div></el-col
      >
    </el-row>
    <el-row :gutter="20" class="interval center">
      <el-col :sapn="24">
        <div class="item grid-content bg-purple">
          <div class="top_title">
            <div class="title_line"></div>
            <span class="text">一次接线图</span>
          </div>
          <div class="line"></div>
          <div class="bottom">
            <div class="bottom_echart">
              <line-charts :chart-data="lineChartData" />
            </div>
          </div></div
      ></el-col>
    </el-row>
    <el-row :gutter="20" class="interval home_bottom">
      <el-col :sapn="24">
        <div class="item grid-content bg-purple">
          <div class="top_title">
            <div class="title_line"></div>
            <span class="text">运行曲线图</span>
          </div>
          <div class="line"></div>
          <div class="bottom">
            <div class="bottom_echart">
              <line-charts :chart-data="lineChartData" />
            </div>
          </div></div
      ></el-col>
    </el-row>
  </div>
</template>
<script setup name="Index">
import LineChart from "./dashboard/currentPower";
import LineCharts from "./dashboard/LineChart";
const version = ref("3.8.5");
const percentage = ref(100);
const dataSourceList = ref([
  {
    label: "当月",
    value: "current",
  },
  {
    label: "累计",
    value: "accumulate",
  },
]);
const leftActiveValue = ref("accumulate");
const activeValue = ref("accumulate");
const lineChartData = ref({
  newVisitis: {
    expectedData: [100, 120, 161, 134, 105, 160, 165],
    actualData: [120, 82, 91, 154, 162, 140, 145],
  },
  messages: {
    expectedData: [200, 192, 120, 144, 160, 130, 140],
    actualData: [180, 160, 151, 106, 145, 150, 130],
  },
  purchases: {
    expectedData: [80, 100, 121, 104, 105, 90, 100],
    actualData: [120, 90, 100, 138, 142, 130, 130],
  },
  shoppings: {
    expectedData: [130, 140, 141, 142, 145, 150, 160],
    actualData: [120, 82, 91, 154, 162, 140, 130],
  },
});
function goTarget(url) {
  window.open(url, "__blank");
}
function searchButton(val, type) {
  console.log(activeValue.value, " activeValue.value");
  console.log(type, "typetypetypetype");
  if (type == "OpticalStorage") {
    leftActiveValue.value = val;
    return;
  }
  activeValue.value = val;
}
</script>

<style scoped lang="scss">
.home {
  height: 100%;
   padding: 0 10px !important;
    background: #001529 !important;
  blockquote {
    padding: 10px 20px;
    margin: 0 0 20px;
    font-size: 17.5px;
    border-left: 5px solid #eee;
  }
  .interval{
      border-bottom: 10px solid #001529;
      
      
    .item{
      width: 100%;
      min-height: 160px;
      box-sizing: border-box;
      border-radius:6px;
      background: #11203B;
    
      .top_title{
        display: flex;
        align-items: center;
        height: 36px;
        line-height: 36px;
        color: #FFFFFF !important;
        justify-content: space-between;
      
        .left{
          display: flex;
          align-items: center;
        }
        .right{
          margin-right: 11px;
          cursor: pointer;
          span{
            border: 1px solid #ccc;
            color:  rgba(255, 255, 255, 0.65);
            background: rgba(255, 255, 255, 0.12);;
            padding: 2px 4px;
          }
        span:nth-last-child(1) {
            border-left:0 !important
}
        }
        .title_line{
          width: 2px;
          height: 16px;
          opacity: 1;
          background: #4997F5;
          margin-left: 2px;
         
        }
        .text{
          margin-left: 10px;
          font-size: 16px;
          color: #FFFFFF;
        }

      }
      .bottom{
        width: 100%;
        display: flex;
        margin-top: 10px;
        justify-content: space-around;
        align-items: center;
     
        .bottom_echart{
          width: 50%;
          min-height:100%
        }
        .bottom_right{
          height: 100%;
          width: 50%;
          margin-top: 10px;
          color: #FFFFFF;
          text-align: right;
          margin-right: 31px;
          .title_text{
            margin-bottom: 10px;
            font-size: 14px;
            .name{
              margin-right: 21px;
            }

          }
          .title_text:nth-last-child(1) {
            margin-bottom:none
}
        }
      }
      .line{
      width: 100%;
      height: 1px;
      background:#FFFFFF ;
      opacity: .3;
    }
    }
.bottom_item{
  text-align: center;
  height: 93px !important;
  .data_line{
    padding-top: 10px;
    position: relative;
    &::before {
      content: " ";
      position: absolute;
      right: -25%;
      top: 50%;
      height: 36px;
      width: 2px;
      background: #FFFFFF;
      opacity: .3;
      z-index: 2;
    }
  }
  .data_lines{
    padding-top: 10px;
  }
  .photovoltaic{
    color: #F9A744;
    font-size: 20px;
  }
  .discharge{
    color:  #46BEFA;
    font-size: 20px;
  }
  .cost{
    color:  #30E0A1;
    font-size: 20px;
  }

  .title{
    color: #FFFFFF;
    margin-top: 21px;
    font-size: 14px;
  }

  .unit{
    opacity: .3;
    font-size: 12px;
    color: #FFFFFF;
    text-align: center;
    margin-top: 3px;
  }
  .last_title {
    color: #FFFFFF;
    margin-top: 15px;
    font-size: 14px;
}
}
   
  }
}
:deep(.el-progress__text){
    font-size: 12px !important;
  }
  :deep(.el-progress-circle){
    width: 54px !important;
    height: 54px !important;
  }
  .active{
    background: rgba(64, 128, 255, 1)!important;
  }
</style>

