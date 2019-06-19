<template>
  <div class="sakushika-result">
    <div class="sakushika-result_main">
      <img src="@/assets/letter_head.jpg" alt>
      <div style="display: flex;align-items: stretch">
        <img src="@/assets/letter_left.jpg" alt>
        <div class="sakushika-result__message">
          <p v-if="step">
            {{titleListFirst[questions.q1[0] - 1]}}{{titleListSecond[questions.q1[1] - 1]}}
          </p>
          <template v-for="(results, questionNumber) in lyricsList">
            <p v-if="step > questionNumber" :key="questionNumber">
              <template v-for="(result, resultIndex) in results">
                <span
                  :key="result"
                  v-if="questions[`q${questionNumber+1}`] === resultIndex+1">
                    {{result}}
                </span>
              </template>
            </p>
          </template>
        </div>
        <img src="@/assets/letter_right.jpg" alt>
      </div>
      <img src="@/assets/letter_foot.jpg" alt>
    </div>
  </div>
</template>

<script>
import { stringify } from "querystring";
export default {
  props: {
    questions: Object,
    step: Number,
    titleListFirst: Array,
    titleListSecond: Array
  },
  data() {
    return {
      displayObject: this.questions
    };
  },
  computed: {
    lyricsList() {
      return [
        [],
        [
          "きみにキスする夢を見た",
          "爪がはがれた夢をみた",
          "俺が世界をとる夢をみた",
          "昔の家に住んでる夢を見た"
        ],
        [
          "気づいたらキミがいない",
          "君がいない４畳半はまるで８畳間",
          "君のメガネがない、君の靴がない。というか君がいない。",
          "リモコンに見とれているうちに夜がきた。"
        ],
        [
          "サヨナラ 大好きな人 サヨナラ",
          "あげたTシャツ よく似合ってる",
          "尻かあたまかあたまか尻か",
          "ここ５年、カレーしか食べていない"
        ],
        [
          "コーラス（きみはロボット　恥を知らないのさ）",
          "コーラス（きみはロボット　僕が上ずっていることに気がつかない）",
          "コーラス（きみはロボット　視力が5.0）",
          "コーラス（きみはロボット　オイルで濡れる）"
        ],
        [
          "手を伸ばしても届かない。手が伸びても届かない。びろーん。",
          "山手線はいつも大崎どまり。終電を間違えてきょうも歩く。",
          "ひとりで選ぶハンバーグ。ひとりで食べる木こり風",
          "ふるえる指先。近所の猫も心配そうに僕を見る"
        ],
        [
          "メールをまってるよー",
          "夜明け過ぎの雨は、僕が雪にかわらせてみせよう",
          "愛の非常口。出口はどこだ。",
          "オー ベイベー やだよーもうー"
        ]
      ];
    }
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, "");
    }
  }
};
</script>

<style scoped>
img {
  user-select: none;
}
.sakushika-result {
  width: 484px;
  margin: 0 auto;
}
.sakushika-result_main {
  font-size: 0;
}
.sakushika-result__message {
  background-image: url('../assets/letter_back.jpg');
  padding: 16px;
  font-size: 12px;
  flex: 1;
  min-height: 150px;
}
.sakushika-result__message p:first-child {
  margin-top: 0;
}
.sakushika-result_build {
  text-align: right;
}
.sakushika-result_share {
  font-size: 12px;
}
.sakushika-result_shareurl {
  width: 100%;
}
.sakushika-result_share {
  display: flex;
  align-items: center;
}
input {
  margin: 4px 10px 4px 0;
  flex: 1;
}
</style>