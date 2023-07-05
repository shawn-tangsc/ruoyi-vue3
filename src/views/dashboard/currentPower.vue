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
      default: "100%",
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
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b}: {c} ({d}%)",
        },
        legend: {
          top: "5%",
          left: "center",
        },
        graphic: {
          type: "text",
          left: "center",
          top: "45%",
          style: {
            text: "哈哈哈哈" + "\n\r" + "合计",
            textAlign: "center",
            fill: "#fff",
            fontSize: 12,
            color: "#fff",
            fontWeight: 700,
          },
        },
        series: [
          {
            name: "",
            type: "pie",
            radius: ["75%", "100%"],
            // center: ["0%", "50%"],
            avoidLabelOverlap: false,
            itemStyle: {
              borderRadius: 5,
              borderColor: "#fff",
              borderWidth: 2,
            },
            label: {
              show: false,
              position: "center",
            },
            emphasis: {
              label: {
                show: true,
                fontSize: 12,
                fontWeight: "bold",
              },
            },
            labelLine: {
              show: false,
            },
            data: [
              {
                value: 1048,
                itemStyle: { color: "#F7931A" },
              },
              { value: 735, itemStyle: { color: "#46BEFA" } },
              { value: 580, itemStyle: { color: "#30E0A1" } },
            ],
          },
        ],
      });
    },
  },
};
</script>
  