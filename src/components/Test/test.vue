<!--词云-->
<style lang="stylus" scoped>
.wordcloud {
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
  <div id="wordcloud">
    <div id="main">
      <wordcloud
        :data="defaultWords"
        nameKey="name"
        valueKey="value"
        :color="myColors"
        :showTooltip="true"
        :wordClick="wordClickHandler"
      ></wordcloud>
    </div>
  </div>
</template>

<script>
import wordcloud from "vue-wordcloud";

export default {
  name: "app",
  components: {
    wordcloud
  },
  methods: {
    wordClickHandler(name, value, vm) {
      console.log("wordClickHandler", name, value, vm);
    }
  },
  data() {
    return {
      radio1: "Trump",
      myColors: ["#1f77b4", "#629fc9", "#94bedb", "#c9e0ef"],
      defaultWords: [
        { name: "Donald", value: 232 },
        { name: "Trump", value: 3002 },
        { name: "failed", value: 402 },
        { name: "American", value: 383 },
        { name: "people", value: 1762 },
        { name: "Joe", value: 4921 },
        { name: "Biden", value: 1566 },
        { name: "vote", value: 480 },
        { name: "lol", value: 168 },
        { name: "Americans", value: 584 },
        { name: "public", value: 153 },
        { name: "democrat", value: 158 },
        { name: "Election", value: 152 },
        { name: "called", value: 524 },
        { name: "President", value: 1800 },
        { name: "xenophobic", value: 222 },
        { name: "action", value: 192 },
        { name: "lives", value: 269 },
        { name: "lost", value: 207 },
        { name: "real", value: 200 },
        { name: "job", value: 372 },
        { name: "die", value: 165 },
        { name: "lies", value: 254 },
        { name: "democrats", value: 518 },
        { name: "China", value: 1246 },
        { name: "coming", value: 206 },
        { name: "leadership", value: 198 },
        { name: "time", value: 875 },
        { name: "crisis", value: 323 },
        { name: "failure", value: 157 },
        { name: "country", value: 633 },
        { name: "calling", value: 150 },
        { name: "travel", value: 721 },
        { name: "ban", value: 315 },
        { name: "care", value: 548 },
        { name: "leader", value: 242 },
        { name: "office", value: 300 },
        { name: "campaign", value: 185 },
        { name: "shut", value: 382 },
        { name: "sentence", value: 156 },
        { name: "bernie", value: 229 },
        { name: "truth", value: 154 },
        { name: "november", value: 176 },
        { name: "media", value: 163 },
        { name: "america", value: 418 },
        { name: "support", value: 247 },
        { name: "hell", value: 161 },
        { name: "obama", value: 916 },
        { name: "deaths", value: 151 },
        { name: "virus", value: 596 },
        { name: "day", value: 397 },
        { name: "sit", value: 205 },
        { name: "lie", value: 257 },
        { name: "true", value: 216 },
        { name: "god", value: 230 },
        { name: "write", value: 532 },
        { name: "tweet", value: 354 },
        { name: "pay", value: 195 },
        { name: "wrong", value: 321 },
        { name: "plan", value: 260 },
        { name: "coronavirus", value: 256 },
        { name: "sleepy", value: 269 },
        { name: "lying", value: 254 },
        { name: "tweets", value: 237 },
        { name: "health", value: 464 },
        { name: "hey", value: 320 },
        { name: "basement", value: 152 },
        { name: "bad", value: 217 },
        { name: "liar", value: 185 },
        { name: "racist", value: 443 },
        { name: "left", value: 245 },
        { name: "prepared", value: 243 },
        { name: "pandemic", value: 650 },
        { name: "news", value: 175 },
        { name: "person", value: 194 },
        { name: "administration", value: 480 },
        { name: "responsible", value: 577 },
        { name: "response", value: 186 },
        { name: "medical", value: 211 },
        { name: "money", value: 320 },
        { name: "dementia", value: 325 },
        { name: "running", value: 195 },
        { name: "nation", value: 232 },
        { name: "national", value: 175 },
        { name: "talk", value: 152 },
        { name: "remember", value: 515 },
        { name: "sir", value: 171 },
        { name: "creepy", value: 171 },
        { name: "tara", value: 201 },
        { name: "reade", value: 180 },
        { name: "swine", value: 166 },
        { name: "flu", value: 208 },
        { name: "call", value: 210 },
        { name: "wrote", value: 269 },
        { name: "blame", value: 273 },
        { name: "government", value: 219 },
        { name: "matter", value: 162 },
        { name: "wait", value: 207 },
        { name: "january", value: 460 },
        { name: "flights", value: 205 },
        { name: "dems", value: 209 },
        { name: "impeachment", value: 283 },
        { name: "bed", value: 182 },
        { name: "talking", value: 207 },
        { name: "house", value: 165 },
        { name: "political", value: 171 },
        { name: "drop", value: 176 },
        { name: "politics", value: 165 },
        { name: "vp", value: 206 },
        { name: "win", value: 160 },
        { name: "guy", value: 171 },
        { name: "family", value: 212 },
        { name: "millions", value: 212 },
        { name: "masks", value: 161 },
        { name: "obamacare", value: 308 },
        { name: "healthcare", value: 477 },
        { name: "insurance", value: 352 },
        { name: "nap", value: 184 },
        { name: "medicare", value: 355 },
        { name: "sleep", value: 193 },
        { name: "told", value: 167 },
        { name: "stay", value: 177 },
        { name: "heart", value: 162 },
        { name: "evidence", value: 351 },
        { name: "shit", value: 179 },
        { name: "party", value: 291 },
        { name: "Pelosi", value: 166 },
        { name: "hunter", value: 171 },
        { name: "prepare", value: 304 },
        { name: "supplies", value: 212 },
        { name: "busy", value: 156 },
        { name: "stockpile", value: 175 }
      ]
    };
  }
};
</script>