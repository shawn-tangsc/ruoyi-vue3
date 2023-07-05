<template>
  <div :class="className" :style="{ height: height, width: width }" />
</template>

<script>
import * as echarts from "echarts";
// require("echarts/theme/macarons"); // echarts theme
import resize from "./mixins/resize";

export default {
  mixins: [resize],
  props: {
    className: {
      type: String,
      default: "chart",
    },
    width: {
      type: String,
      default: "100%",
    },
    height: {
      type: String,
      default: "350px",
    },
    autoResize: {
      type: Boolean,
      default: true,
    },
    chartData: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      chart: null,
    };
  },
  watch: {
    chartData: {
      deep: true,
      handler(val) {
        this.setOptions(val);
      },
    },
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart();
    });
  },
  beforeDestroy() {
    if (!this.chart) {
      return;
    }
    this.chart.dispose();
    this.chart = null;
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$el, "macarons");
      this.setOptions(this.chartData);
    },
    setOptions({ expectedData, actualData } = {}) {
      this.chart.setOption({
        xAxis: [
          {
            type: "category",
            boundaryGap: false,
            data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
          },
        ],
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true,
        },
        tooltip: {
          trigger: "axis",

          axisPointer: {
            type: "cross",
            label: {
              backgroundColor: "#6a7985",
            },
          },
          padding: [5, 10],
        },
        yAxis: [
          {
            type: "value",
          },
        ],
        legend: {
          data: ["Email", "Union Ads", "Video Ads", "Direct", "Search Engine"],
        },
        toolbox: {
          feature: {
            saveAsImage: {},
          },
        },
        series: [
          {
            stack: "Total",
            areaStyle: {},
            name: "expected",
            // itemStyle: {
            //   normal: {
            //     color: "#FF005A",
            //     lineStyle: {
            //       color: "#FF005A",
            //       width: 2,
            //     },
            //   },
            // },
            emphasis: {
              focus: "series",
            },
            smooth: true,
            type: "line",
            data: [200, 192, 120, 144, 160, 130, 140],
            animationDuration: 2800,
            animationEasing: "quadraticOut",
          },
          {
            stack: "Total",
            areaStyle: {},
            name: "actual",
            smooth: true,
            type: "line",
            emphasis: {
              focus: "series",
            },
            // itemStyle: {
            //   normal: {
            //     color: "#3888fa",
            //     lineStyle: {
            //       color: "#3888fa",
            //       width: 2,
            //     },
            //     areaStyle: {
            //       color: "#f3f8ff",
            //     },
            //   },
            // },
            data: [80, 100, 121, 104, 105, 90, 100],
            animationDuration: 2800,
            animationEasing: "quadraticOut",
          },
        ],
      });
    },
  },
};
</script>
