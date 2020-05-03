<!-- 柱状图 -->
<style lang="stylus" scoped>
.columnChart {
  height: 800px;
  background: url('../../assets/bg.jpg') no-repeat;
  background-size: 100% 100%;
  color: white;

  .main {
    width: 100%;
    height: calc(100% - 100px);
    margin-top: -15px;
  }
}
</style>

<template>
  <div class="columnChart">
    <v-header :name="name" :legendArr="legendArr" :myChart="myChart"></v-header>
    <!-- <v-filter :myChart="myChart" v-if="myChart._dom"></v-filter> -->
    <div class="main" style="margin-top:30px"></div>
  </div>
</template>

<script>
import echarts from "echarts";
import header from "components/header/header";
import filter from "components/filter/filter";

export default {
  data() {
    return {
      legendArr: [],
      color: this.$store.state.color,
      myChart: {},
      name: "Sources"
    };
  },
  methods: {
    _chartInit() {
      this.legendArr = this.myChart.getOption().series;
      this.legendArr.forEach(data => {
        data.selected = true;
      });
      this.$root.charts.push(this.myChart);
      window.addEventListener(
        "resize",
        function() {
          this.myChart.resize();
        }.bind(this)
      );
    }
  },
  components: {
    "v-header": header,
    "v-filter": filter
  },
  mounted() {
    // 基于准备好的dom，初始化echarts实例
    this.myChart = echarts.init(document.querySelector(".columnChart .main"));
    this.myChart.setOption({
      title: {
        show: false
      },
      tooltip: {
        trigger: "axis"
      },
      legend: {
        show: false
      },
      toolbox: {
        show: false
      },
      color: this.color,
      calculable: true,
      xAxis: [
        {
          name: "Sources",
          type: "category",
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          nameTextStyle: {
            color: "rgba(255, 255, 255, 0.69)"
          },
          axisLabel: {
            textStyle: {
              color: "white"
            }
          },
          data: ["Trump", "Biden"]
        }
      ],
      yAxis: [
        {
          axisLine: {
            show: false
          },
          nameLocation: "end",
          nameGap: 20,
          nameRotate: 0,
          axisTick: {
            show: false
          },
          splitLine: {
            lineStyle: {
              color: ["rgba(230, 230, 230, 0.2)"]
            }
          },
          axisLabel: {
            textStyle: {
              color: "white",
              fontSize: 14
            }
          },
          name: "Number",
          type: "value",
          nameTextStyle: {
            color: "rgba(255, 255, 255, 0.69)"
          }
        }
      ],
      series: [
        {
          name: "Android",
          type: "bar",
          data: [10825, 6022],
          barWidth: 16,
          barGap: 0
        },
        {
          name: "Iphone",
          type: "bar",
          data: [14244, 9362],
          barWidth: 16,
          barGap: 0
        },
        {
          name: "Ipad",
          type: "bar",
          data: [2083, 1143],
          barWidth: 16,
          barGap: 0
        },
        {
          name: "Web",
          type: "bar",
          data: [7787, 4959],
          barWidth: 16,
          barGap: 0
        },
        {
          name: "TweetDeck",
          type: "bar",
          data: [89, 35],
          barWidth: 16,
          barGap: 0
        },
        {
          name: "Mac",
          type: "bar",
          data: [17, 13],
          barWidth: 16,
          barGap: 0
        },
        {
          name: "Other",
          type: "bar",
          data: [97, 31],
          barWidth: 16,
          barGap: 0
        }
      ]
    });
    this._chartInit();
  }
};
</script>
