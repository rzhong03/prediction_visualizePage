<!-- 散点图 -->
<style lang="stylus" scoped>
.point {
  background: url('../../assets/bg.jpg') no-repeat;
  background-size: 100% 100%;

  .main {
    height: calc(100% - 120px);
    width: 100%;
    transition: all 0.5s linear;
  }
}

.filter {
  position: relative;
  display: flex;
  padding: 10px 0 0 28px;
  font-size: 12px;
  line-height: 11px;
  color: white;
  z-index: 9999;

  .myCalendar {
    left: auto !important;
  }

  input {
    background: transparent;
    border: none;
    color: white;
  }

  .timeText {
    opacity: 0.69;
    padding-right: 7px;
  }

  .startTime {
    display: inline-block;
  }

  .endTime {
    display: inline-block;
    padding-left: 42px;
  }

  .el-date-editor {
    width: 55%;
  }

  .products {
    position: absolute;
    display: inline-block;
    right: 15px;

    .all {
      display: inline-block;
      margin-right: 18px;

      .v-checkbox {
        position: relative;
        top: 2px;
        left: -3px;
      }
    }

    .pro {
      float: right;
      padding: 2px 25px 2px 2px;

      .arrow {
        position: absolute;
        width: 6px;
        height: 6px;
        margin-left: 10px;
        border-left: 2px solid white;
        border-bottom: 2px solid white;
        transform: rotate(-45deg);
      }
    }
  }

  .pro_list {
    position: absolute;
    right: 22px;
    width: 102px;
    text-align: left;
    background: #1e3642;
    font-size: 14px;
    margin-top: 22px;
    /* max-height 180px */
    overflow: hidden;
    z-index: 9;

    li {
      height: 36px;
      line-height: 36px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);

      &:last-child {
        border: none;
      }

      .v-checkbox {
        left: 8px;
      }

      .name {
        position: absolute;
        display: inline-block;
        right: 8px;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        width: 70px;
      }
    }
  }
}
</style>

<template lang="html">

<div class="point">

  
  <v-header :name="name" :legendArr="legendArr" :myChart="myChart">
  </v-header>
      <el-radio-group class="filter" fill="#53868B" size="small" v-model="radio1" style="float:right;padding-right:10px;margin-top:-50px" @change="changeOption">
      <el-radio-button label="Trump"></el-radio-button>
      <el-radio-button label="Biden"></el-radio-button>
    </el-radio-group>
 
  <!-- <v-filter :myChart="myChart" v-if="myChart._dom"></v-filter> -->
  <div class="main"></div>
</div>
</template>

<script>
import axios from "axios";
import echarts from "echarts";
import usa from "echarts/map/js/usa";
import header from "components/header/header";
import filter from "components/filter/filter";
export default {
  created() {
    this._getCityData();
  },
  data() {
    return {
      legendArr: [],
      color: this.$store.state.color,
      myChart: {},
      geoCoordMap: {},
      name: "Sentiment",
      radio1: "Trump",
      options: {},
      option_data: [
        {
          name: "Alaska",
          value: 619.0476
        },
        {
          name: "Alabama",
          value: 182.04292
        },
        {
          name: "Arkansas",
          value: 367.13809
        },
        {
          name: "Arizona",
          value: 98.02852
        },
        {
          name: "California",
          value: 174.84806
        },
        {
          name: "Colorado",
          value: 14.55439
        },
        {
          name: "Connecticut",
          value: 763.98478
        },
        {
          name: "District of Columbia",
          value: 164.03574
        },
        {
          name: "Florida",
          value: 181.91924
        },
        {
          name: "Georgia",
          value: 295.57072
        },
        {
          name: "Hawaii",
          value: 52.12147
        },
        {
          name: "Illinois",
          value: 200.76762
        },
        {
          name: "Indiana",
          value: 283.5283
        },
        {
          name: "Kansas",
          value: -72.3778
        },
        {
          name: "Kentucky",
          value: -395.11261
        },
        {
          name: "Louisiana",
          value: 147.93125
        },
        {
          name: "Massachusetts",
          value: 69.91261
        },
        {
          name: "Maryland",
          value: -42.11264
        },
        {
          name: "Maine",
          value: 335.25588
        },
        {
          name: "Michigan",
          value: 2221.1784
        },
        {
          name: "Minnesota",
          value: -269.6894
        },
        {
          name: "Missouri",
          value: -5.93184
        },
        {
          name: "Mississippi",
          value: 4.28391
        },
        {
          name: "Montana",
          value: -2611.11111
        },
        {
          name: "North Carolina",
          value: 131.37189
        },
        {
          name: "North Dakota",
          value: 543.07387
        },
        {
          name: "Nebraska",
          value: 340.3957
        },
        {
          name: "New Hampshire",
          value: -178.44379
        },
        {
          name: "New Jersey",
          value: -10.88318
        },
        {
          name: "New Mexico",
          value: -294.99495
        },
        {
          name: "Nevada",
          value: 218.10009
        },
        {
          name: "New York",
          value: 104.47829
        },
        {
          name: "Ohio",
          value: 98.36234
        },
        {
          name: "Oklahoma",
          value: 640.28358
        },
        {
          name: "Oregon",
          value: 245.59983
        },
        {
          name: "Pennsylvania",
          value: 221.31232
        },
        {
          name: "Rhode Island",
          value: 614.17193
        },
        {
          name: "South Carolina",
          value: -288.14314
        },
        {
          name: "South Dakota",
          value: 973.09205
        },
        {
          name: "Tennessee",
          value: -309.03127
        },
        {
          name: "Texas",
          value: 238.95242
        },
        {
          name: "USA",
          value: 152.94615
        },
        {
          name: "Utah",
          value: 209.7196
        },
        {
          name: "Virginia",
          value: 256.15034
        },
        {
          name: "Washington",
          value: -22.86448
        },
        {
          name: "Wisconsin",
          value: 217.6238
        },
        {
          name: "West Virginia",
          value: -669.56407
        },
        {
          name: "Wyoming",
          value: 250
        },
        {
          name: "Others",
          value: 162.9875
        }
      ]
    };
  },
  methods: {
    _chartInit(options) {
      this.myChart = echarts.init(document.querySelector(".point .main"));
      console.log(options);
      this.myChart.setOption(this.options);
      this.$root.charts.push(this.myChart);
      window.addEventListener(
        "resize",
        function() {
          this.myChart.resize();
        }.bind(this)
      );
    },
    _getCityData() {
      axios.get("static/data/cityData.json").then(res => {
        this.geoCoordMap = res.data;
        this.$nextTick(() => {
          this._getMyChart();
        });
      });
    },
    _getMyChart() {
      // axios.get("static/data/point/testData.json").then(res => {
      this.options = {
        // backgroundColor: '#404a59',
        title: {
          show: false
        },
        tooltip: {
          trigger: "item",
          showDelay: 0,
          transitionDuration: 0.2,
          formatter: function(params) {
            var value = (params.value + "").split(".");
            value = value[0].replace(/(\d{1,3})(?=(?:\d{3})+(?!\d))/g, "$1,");
            return params.seriesName + "<br/>" + params.name + ": " + value;
          }
        },
        visualMap: {
          show: false,
          left: "left",
          min: -1000,
          max: 1000,
          inRange: {
            color: ["#feca57", "#b33939"]
          },
          text: ["High", "Low"], // 文本，默认为数值文本
          textStyle: {
            color: "#fff"
          },
          calculable: true
        },
        geo: {
          // map: "usa",
          // type: "map",
          roam: true,
          label: {
            emphasis: {
              show: true
            }
          },
          zoom: 1.5,
          // top: 50,
          itemStyle: {
            normal: {
              color: "white",
              opacity: 0.7,
              borderColor: "rgba(0, 0, 0, 1)"
            },
            emphasis: {
              color: "blue"
            }
          }
        },
        toolbox: {
          show: false,
          left: "left",
          top: "top",
          feature: {
            dataView: { readOnly: false },
            restore: {},
            saveAsImage: {}
          }
        },
        series: [
          {
            name: "",
            type: "map",
            roam: true,
            map: "usa",
            zoom: 1.4,
            left: 150,
            top: 80,
            emphasis: {
              label: {
                show: true
              }
            },
            data: this.option_data
          }
        ]
      };
      this._chartInit(this.options);
      // });
    },

    changeOption() {
      if (this.radio1 === "Trump") {
        console.log("Trump");
        this.option_data = [
          {
            name: "Alaska",
            value: 619.0476
          },
          {
            name: "Alabama",
            value: 182.04292
          },
          {
            name: "Arkansas",
            value: 367.13809
          },
          {
            name: "Arizona",
            value: 98.02852
          },
          {
            name: "California",
            value: 174.84806
          },
          {
            name: "Colorado",
            value: 14.55439
          },
          {
            name: "Connecticut",
            value: 763.98478
          },
          {
            name: "District of Columbia",
            value: 164.03574
          },
          {
            name: "Florida",
            value: 181.91924
          },
          {
            name: "Georgia",
            value: 295.57072
          },
          {
            name: "Hawaii",
            value: 52.12147
          },
          {
            name: "Illinois",
            value: 200.76762
          },
          {
            name: "Indiana",
            value: 283.5283
          },
          {
            name: "Kansas",
            value: -72.3778
          },
          {
            name: "Kentucky",
            value: -395.11261
          },
          {
            name: "Louisiana",
            value: 147.93125
          },
          {
            name: "Massachusetts",
            value: 69.91261
          },
          {
            name: "Maryland",
            value: -42.11264
          },
          {
            name: "Maine",
            value: 335.25588
          },
          {
            name: "Michigan",
            value: 2221.1784
          },
          {
            name: "Minnesota",
            value: -269.6894
          },
          {
            name: "Missouri",
            value: -5.93184
          },
          {
            name: "Mississippi",
            value: 4.28391
          },
          {
            name: "Montana",
            value: -2611.11111
          },
          {
            name: "North Carolina",
            value: 131.37189
          },
          {
            name: "North Dakota",
            value: 543.07387
          },
          {
            name: "Nebraska",
            value: 340.3957
          },
          {
            name: "New Hampshire",
            value: -178.44379
          },
          {
            name: "New Jersey",
            value: -10.88318
          },
          {
            name: "New Mexico",
            value: -294.99495
          },
          {
            name: "Nevada",
            value: 218.10009
          },
          {
            name: "New York",
            value: 104.47829
          },
          {
            name: "Ohio",
            value: 98.36234
          },
          {
            name: "Oklahoma",
            value: 640.28358
          },
          {
            name: "Oregon",
            value: 245.59983
          },
          {
            name: "Pennsylvania",
            value: 221.31232
          },
          {
            name: "Rhode Island",
            value: 614.17193
          },
          {
            name: "South Carolina",
            value: -288.14314
          },
          {
            name: "South Dakota",
            value: 973.09205
          },
          {
            name: "Tennessee",
            value: -309.03127
          },
          {
            name: "Texas",
            value: 238.95242
          },
          {
            name: "USA",
            value: 152.94615
          },
          {
            name: "Utah",
            value: 209.7196
          },
          {
            name: "Virginia",
            value: 256.15034
          },
          {
            name: "Washington",
            value: -22.86448
          },
          {
            name: "Wisconsin",
            value: 217.6238
          },
          {
            name: "West Virginia",
            value: -669.56407
          },
          {
            name: "Wyoming",
            value: 250
          },
          {
            name: "Others",
            value: 162.9875
          }
        ];
        this._getMyChart();
      } else {
        console.log("Biden");
        this.option_data = [
          {
            name: "Alaska",
            value: -3333.33333
          },
          {
            name: "Alabama",
            value: 362.99918
          },
          {
            name: "Arkansas",
            value: -297.73026
          },
          {
            name: "Arizona",
            value: 349.07938
          },
          {
            name: "California",
            value: 242.25309
          },
          {
            name: "Colorado",
            value: 269.59971
          },
          {
            name: "Connecticut",
            value: 28.73594
          },
          {
            name: "District of Columbia",
            value: -79.09469
          },
          {
            name: "Florida",
            value: 88.19165
          },
          {
            name: "Georgia",
            value: 383.28408
          },
          {
            name: "Hawaii",
            value: 60.72473
          },
          {
            name: "Idaho",
            value: 450.01856
          },
          {
            name: "Iowa",
            value: 509.67361
          },
          {
            name: "Illinois",
            value: -132.79888
          },
          {
            name: "Indiana",
            value: -52.80178
          },
          {
            name: "Kansas",
            value: -52.80178
          },
          {
            name: "Kentucky",
            value: -4.31328
          },
          {
            name: "Louisiana",
            value: 262.85508
          },
          {
            name: "Maine",
            value: -54.82026
          },
          {
            name: "Maryland",
            value: -54.82026
          },
          {
            name: "Massachusetts",
            value: 220.84017
          },
          {
            name: "Michigan",
            value: 277.4297
          },
          {
            name: "Minnesota",
            value: 600.50548
          },
          {
            name: "Mississippi",
            value: 400.2425
          },
          {
            name: "Missouri",
            value: 147.38773
          },
          {
            name: "Montana",
            value: 214.28571
          },
          {
            name: "Nebraska",
            value: 555.14686
          },
          {
            name: "Nevada",
            value: 12.75471
          },
          {
            name: "New Hampshire",
            value: 576.82292
          },
          {
            name: "New Jersey",
            value: 272.18542
          },
          {
            name: "New Mexico",
            value: -637.41978
          },
          {
            name: "New York",
            value: 225.28101
          },
          {
            name: "North Carolina",
            value: 96.3173
          },
          {
            name: "North Dakota",
            value: 403.88889
          },
          {
            name: "Ohio",
            value: 179.10598
          },
          {
            name: "Oklahoma",
            value: 492.85027
          },
          {
            name: "Oregon",
            value: 269.19098
          },
          {
            name: "Pennsylvania",
            value: 284.13547
          },
          {
            name: "Rhode Island",
            value: 188.12004
          },
          {
            name: "South Carolina",
            value: -3.91435
          },
          {
            name: "Tennessee",
            value: 312.53696
          },
          {
            name: "Texas",
            value: 35.91015
          },
          {
            name: "Utah",
            value: 172.93804
          },
          {
            name: "Vermont",
            value: 172.93804
          },
          {
            name: "Virginia",
            value: 172.93804
          },
          {
            name: "Washington",
            value: 423.41766
          },
          {
            name: "West Virginia",
            value: 1699.04762
          },
          {
            name: "Wisconsin",
            value: 104.24051
          },
          {
            name: "Wyoming",
            value: 3333.33333
          }
        ];
        this._getMyChart();
      }
    }
  },
  components: {
    "v-header": header,
    "v-filter": filter
  }
};
</script>
