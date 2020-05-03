<!-- 层叠柱状图 -->
<style lang="stylus" scoped>
.line {
  height: 1000px;
  background: url('../../assets/bg.jpg') no-repeat;
  background-size: 100% 100%;

  .main {
    width: 100%;
    height: calc(100% - 100px);
    margin-top: -15px;
  }
}
</style>

<template>
  <div class="line">
    <v-header :name="name" :legendArr="legendArr" :myChart="myChart"></v-header>
    <el-radio-group
      fill="#53868B"
      size="small"
      v-model="radio1"
      style="float:right;padding-right:10px;margin-top:-40px"
      @change="changeOption"
    >
      <el-radio-button label="Trump"></el-radio-button>
      <el-radio-button label="Biden"></el-radio-button>
    </el-radio-group>
    <!-- <v-filter :myChart="myChart" v-if="myChart._dom"></v-filter> -->
    <!-- margin="0"
        wordPadding="1"
    fontSize="[5,40]"-->
    <div class="main">
      <wordcloud
        style="margin-top:8%"
        :data="defaultWords"
        nameKey="name"
        valueKey="value"
        :color="myColors"
        :fontSize="[5,50]"
        :showTooltip="true"
        :wordClick="wordClickHandler"
      ></wordcloud>
    </div>
  </div>
</template>

<script>
import echarts from "echarts";
import header from "components/header/header";
import filter from "components/filter/filter";
import wordcloud from "vue-wordcloud";

export default {
  data() {
    return {
      legendArr: [],
      color: this.$store.state.color,
      myChart: {},
      name: "WordCloud",
      radio1: "Trump",
      myColors: ["#1f77b4", "#629fc9", "#94bedb", "#c9e0ef"],
      defaultWords: [
        {
          value: "6",
          name: "fucking job"
        },
        {
          value: "8.5",
          name: "medical professionals"
        },
        {
          value: "8",
          name: "facing reality"
        },
        {
          value: "8",
          name: "doctors nurses"
        },
        {
          value: "4.5",
          name: "cheater"
        },
        {
          value: "4.333333333",
          name: "criticise "
        },
        {
          value: "4.25",
          name: "pandemic "
        },
        {
          value: "4.25",
          name: "leaks "
        },
        {
          value: "4.25",
          name: "rallying "
        },
        {
          value: "4.882400699",
          name: "find cures"
        },
        {
          value: "3.122339406",
          name: "diseases "
        },
        {
          value: "0.162938651",
          name: "good pat"
        },
        {
          value: "2.613465142",
          name: "fellow americans"
        },
        {
          value: "1.548472395",
          name: "social distancing"
        },
        {
          value: "0.318983436",
          name: "falae vers"
        },
        {
          value: "7.279867273",
          name: "positive impact"
        },
        {
          value: "0.194026915",
          name: "recommendedmy proposal"
        },
        {
          value: "0.683699676",
          name: "bay trump"
        },
        {
          value: "0.255531715",
          name: "finally grace"
        },
        {
          value: "4.126220625",
          name: "car manufacturers"
        },
        {
          value: "0.890618626",
          name: "oval office"
        },
        {
          value: "2.542749533",
          name: "great idea"
        },
        {
          value: "2.370430218",
          name: "bankrupt america"
        },
        {
          value: "0.876984349",
          name: "disgusting match"
        },
        {
          value: "2.483325768",
          name: "crotch rot"
        },
        {
          value: "0.036159678",
          name: "gun shows"
        },
        {
          value: "0.275647515",
          name: "killer profit"
        },
        {
          value: "0.477334229",
          name: "car companies"
        },
        {
          value: "2.517051104",
          name: "def fluid"
        },
        {
          value: "1.506333967",
          name: "southern california"
        },
        {
          value: "0.595046899",
          name: "save millions"
        },
        {
          value: "4.484205363",
          name: "gambling enterprises"
        },
        {
          value: "2.378938703",
          name: "malaria drug"
        },
        {
          value: "2.749668708",
          name: "real leader"
        },
        {
          value: "3.719143803",
          name: "particulate filters"
        },
        {
          value: "1.23908443",
          name: "environmentally friendly"
        },
        {
          value: "3.032413071",
          name: "covid issue"
        },
        {
          value: "0.941898144",
          name: "luxury boondoggles"
        },
        {
          value: "1.175779799",
          name: "diesel engines"
        },
        {
          value: "3.243830632",
          name: "sued california"
        },
        {
          value: "0.252900729",
          name: "ur comment"
        },
        {
          value: "4.946860112",
          name: "distributing goods"
        },
        {
          value: "1.891418415",
          name: "chuck schumer"
        },
        {
          value: "0.752551872",
          name: "fearless leader"
        },
        {
          value: "0.832279989",
          name: "heartless pos"
        },
        {
          value: "4.700643187",
          name: "foolish executives"
        },
        {
          value: "2.823027989",
          name: "needed direction"
        },
        {
          value: "3.389431172",
          name: "started late"
        },
        {
          value: "2.273724603",
          name: "fat phony"
        }
      ]
    };
  },
  methods: {
    wordClickHandler(name, value, vm) {
      console.log("wordClickHandler", name, value, vm);
    },
    changeOption() {
      if (this.radio1 === "Trump") {
        this.defaultWords = [
          {
            value: "6",
            name: "fucking job"
          },
          {
            value: "8.5",
            name: "medical professionals"
          },
          {
            value: "8",
            name: "facing reality"
          },
          {
            value: "8",
            name: "doctors nurses"
          },
          {
            value: "4.5",
            name: "cheater"
          },
          {
            value: "4.333333333",
            name: "criticise "
          },
          {
            value: "4.25",
            name: "pandemic "
          },
          {
            value: "4.25",
            name: "leaks "
          },
          {
            value: "4.25",
            name: "rallying "
          },
          {
            value: "4.882400699",
            name: "find cures"
          },
          {
            value: "3.122339406",
            name: "diseases "
          },
          {
            value: "0.162938651",
            name: "good pat"
          },
          {
            value: "2.613465142",
            name: "fellow americans"
          },
          {
            value: "1.548472395",
            name: "social distancing"
          },
          {
            value: "0.318983436",
            name: "falae vers"
          },
          {
            value: "3.279867273",
            name: "positive impact"
          },
          {
            value: "0.194026915",
            name: "recommendedmy proposal"
          },
          {
            value: "0.683699676",
            name: "bay trump"
          },
          {
            value: "0.255531715",
            name: "finally grace"
          },
          {
            value: "4.126220625",
            name: "car manufacturers"
          },
          {
            value: "0.890618626",
            name: "oval office"
          },
          {
            value: "2.542749533",
            name: "great idea"
          },
          {
            value: "2.370430218",
            name: "bankrupt america"
          },
          {
            value: "0.876984349",
            name: "disgusting match"
          },
          {
            value: "2.483325768",
            name: "crotch rot"
          },
          {
            value: "0.036159678",
            name: "gun shows"
          },
          {
            value: "0.275647515",
            name: "killer profit"
          },
          {
            value: "0.477334229",
            name: "car companies"
          },
          {
            value: "2.517051104",
            name: "def fluid"
          },
          {
            value: "1.506333967",
            name: "southern california"
          },
          {
            value: "0.595046899",
            name: "save millions"
          },
          {
            value: "4.484205363",
            name: "gambling enterprises"
          },
          {
            value: "2.378938703",
            name: "malaria drug"
          },
          {
            value: "2.749668708",
            name: "real leader"
          },
          {
            value: "3.719143803",
            name: "particulate filters"
          },
          {
            value: "1.23908443",
            name: "environmentally friendly"
          },
          {
            value: "3.032413071",
            name: "covid issue"
          },
          {
            value: "0.941898144",
            name: "luxury boondoggles"
          },
          {
            value: "1.175779799",
            name: "diesel engines"
          },
          {
            value: "3.243830632",
            name: "sued california"
          },
          {
            value: "0.252900729",
            name: "ur comment"
          },
          {
            value: "4.946860112",
            name: "distributing goods"
          },
          {
            value: "1.891418415",
            name: "chuck schumer"
          },
          {
            value: "0.752551872",
            name: "fearless leader"
          },
          {
            value: "0.832279989",
            name: "heartless pos"
          },
          {
            value: "4.700643187",
            name: "foolish executives"
          },
          {
            value: "2.823027989",
            name: "needed direction"
          },
          {
            value: "3.389431172",
            name: "started late"
          },
          {
            value: "2.273724603",
            name: "fat phony"
          }
        ];
      } else {
        this.defaultWords = [
          {
            name: "medical caregivers",
            value: "7"
          },
          {
            name: "success rate",
            value: "8"
          },
          {
            name: "china remember sleepy",
            value: "9"
          },
          {
            name: "democratic governors",
            value: "9"
          },
          {
            name: "public service",
            value: "3.285432077"
          },
          {
            name: "full effect",
            value: "4.80756757"
          },
          {
            name: "reality tv",
            value: "4.92787844"
          },
          {
            name: "blonde hairs",
            value: "1.878659793"
          },
          {
            name: "putin trolls",
            value: "3.558156603"
          },
          {
            name: "country pretty",
            value: "0.378260782"
          },
          {
            name: "real disconnect",
            value: "2.826874012"
          },
          {
            name: "real test",
            value: "4.897300096"
          },
          {
            name: "produce meat",
            value: "0.440188767"
          },
          {
            name: "video clip",
            value: "2.735484468"
          },
          {
            name: "bogus facts",
            value: "5.276352819"
          },
          {
            name: "maga bots",
            value: "0.827501182"
          },
          {
            name: "cyber bullying",
            value: "0.336771286"
          },
          {
            name: "find time",
            value: "2.615032763"
          },
          {
            name: "travel ban",
            value: "2.650411228"
          },
          {
            name: "speedy trial",
            value: "3.821048901"
          },
          {
            name: "lose loved",
            value: "7.660228668"
          },
          {
            name: "class action",
            value: "3.697844376"
          },
          {
            name: "worst president",
            value: "6.54972541"
          },
          {
            name: "donald trump",
            value: "1.672571718"
          },
          {
            name: "pure incompetence",
            value: "2.780871569"
          },
          {
            name: "trump checks",
            value: "1.735755198"
          },
          {
            name: "rapey hands",
            value: "0.944311971"
          },
          {
            name: "h1n1 epademic",
            value: "1.103566305"
          },
          {
            name: "great ad",
            value: "4.178455489"
          },
          {
            name: "social media",
            value: "3.908829661"
          },
          {
            name: "epic crisis",
            value: "0.856874937"
          },
          {
            name: "biggest sigh",
            value: "5.930465778"
          },
          {
            name: "failing america",
            value: "2.317846958"
          },
          {
            name: "med supply",
            value: "4.632075222"
          },
          {
            name: "protect ",
            value: "3.665540073"
          },
          {
            name: "tax payers",
            value: "0.62365417"
          },
          {
            name: "hair biden",
            value: "1.093739415"
          },
          {
            name: "march 6th",
            value: "1.016701376"
          },
          {
            name: "true today",
            value: "1.527835713"
          },
          {
            name: "waste kits",
            value: "2.612786703"
          },
          {
            name: "simply wrong",
            value: "2.055906503"
          },
          {
            name: "coronavirus started",
            value: "3.554093744"
          },
          {
            name: "blank check",
            value: "1.698752166"
          },
          {
            name: "clueless seal",
            value: "1.857032638"
          },
          {
            name: "people shouldn",
            value: "0.990390893"
          },
          {
            name: "highest bidders",
            value: "2.050131945"
          },
          {
            name: "mitch mcconnell",
            value: "1.073397305"
          },
          {
            name: "china lied",
            value: "6.149886393"
          },
          {
            name: "stupid questions",
            value: "3.176633292"
          },
          {
            name: "great leader",
            value: "0.208217107"
          }
        ];
      }
    }
  },
  components: {
    "v-header": header,
    "v-filter": filter,
    wordcloud
  },
  mounted() {}
};
</script>
