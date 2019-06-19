<template>
  <div id="app">
    <span v-if="step < 7">
      <b>step{{step+1}}</b>
    </span>
    <SelectTitle
      key="start"
      v-if="step === 0"
      @start="handleStart"
      :value="[questions.q1[0],questions.q1[1]]"
      :titleListFirst="titleListFirst"
      :titleListSecond="titleListSecond"
    />
    <SelectLyrics
      key="lyrics"
      v-if="step === 1"
      v-model="questions.q2"
      @next="handleNext"
      :message="messageList[0]"
      :choices="choiceList[0]"
    />
    <SelectLyrics
      key="lyrics"
      v-if="step === 2"
      v-model="questions.q3"
      @next="handleNext"
      :message="messageList[1]"
      :choices="choiceList[1]"
    />
    <SelectLyrics
      key="lyrics"
      v-if="step === 3"
      v-model="questions.q4"
      @next="handleNext"
      :message="messageList[2]"
      :choices="choiceList[2]"
    />
    <SelectLyrics
      key="lyrics"
      v-if="step === 4"
      v-model="questions.q5"
      @next="handleNext"
      :message="messageList[3]"
      :choices="choiceList[3]"
    />
    <SelectLyrics
      key="lyrics"
      v-if="step === 5"
      v-model="questions.q6"
      @next="handleNext"
      :message="messageList[4]"
      :choices="choiceList[4]"
    />
    <SelectLyrics
      key="lyrics"
      v-if="step === 6"
      v-model="questions.q7"
      @next="handleNext"
      :message="messageList[5]"
      :choices="choiceList[5]"
    />
    <Result
      key="result"
      v-if="step === 7"
      @end="handleEnd"
      :questions="questions"
    />
    <DisplayLyrics
      key="display"
      :questions="questions"
      :step="step"
      :titleListFirst="titleListFirst"
      :titleListSecond="titleListSecond"
    />
  </div>
</template>

<script>
import SelectTitle from "./components/SelectTitle.vue";
import SelectLyrics from "./components/SelectLyrics.vue";
import DisplayLyrics from "./components/DisplayLyrics.vue";
import Result from "./components/Result.vue";

export default {
  name: "app",
  data() {
    return {
      step: 0,
      questions: {
        q1: [1, 1],
        q2: 1,
        q3: 1,
        q4: 1,
        q5: 1,
        q6: 1,
        q7: 1
      }
    }
  },
  components: {
    SelectTitle,
    SelectLyrics,
    DisplayLyrics,
    Result
  },
  methods: {
    handleNext() {
      this.step++;
    },
    handleStart(startData) {
      this.questions.q1[0] = startData.index1;
      this.questions.q1[1] = startData.index2;
      this.handleNext();
    },
    handleEnd() {
      console.log("handled")
      this.step = 0;
    }
  },
  computed: {
    titleListFirst() {
      return [
        "愛の",
        "涙の",
        "始まりはいつも",
        "ドラマチック",
        "心に咲いた",
        "世界にひとつだけの"
      ];
    },
    titleListSecond() {
      return ["森", "ロックンロール", "終着駅", "レイニーデイ", "肉", "花束"];
    },
    messageList() {
      return [
        "歌いだし",
        "続くフレーズは",
        "サビです",
        "コーラス",
        "もいちどサビ",
        "しめは？"
      ];
    },
    choiceList() {
      return [
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
          "きみはロボット　恥を知らないのさ",
          "きみはロボット　僕が上ずっていることに気がつかない",
          "きみはロボット　視力が5.0",
          "きみはロボット　オイルで濡れる"
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
    },
    lyricsList() {
      return [
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
    },
    scoreList() {
      return [
        [20, 15, 12, 19],
        [15, 20, 12, 10],
        [10, 12, 20, 18],
        [12, 10, 18, 20],
        [7, 4, 8, 10],
        [1, 6, 3, 9]
      ];
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
