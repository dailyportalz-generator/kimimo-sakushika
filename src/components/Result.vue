<template>
  <form @submit.prevent="handleEnd" class="result">
    <p class="kansei">完成</p>
    <p class="rank">あなたが書いた歌はオリコンで {{this.getRank(questions)}} 位になりました。</p>
    <p class="description">{{this.getDescription(questions)}}</p>
    <div class="replay">
      <p v-if="getRank(questions) <= 10">
        <button type="submit">やり直す</button>
      </p>
      <p v-else>
        <button type="submit">気にいらないからやり直す</button>
      </p>
    </div>
  </form>
</template>

<script>
export default {
  props: {
    questions: Object,
    rank: Number,
    score: Number
  },
  computed: {
    descriptionList() {
      return [
        "おめでとう！これで人気作詞家の仲間入りです。夢の印税生活。カラオケでうたわれてもお金がはいってきます。人気が落ちないうちに2作目、3作目も出してみよう。",
        "ベスト10入りも直前です。人気グループがシングル10枚同時発売とかそんなアクシデントさえなければ大丈夫です。",
        "もうすぐベスト10入りです。選んだ詞をもういちど見直すか、バンドのさえないドラムをメンバーチェンジさせてしまうかすれば野望達成も夢ではありません。",
        "ザ･ベスト10でいえば「もうすぐベスト10」に登場する順位です。これ以上あがると昔からのファンが去っていってしまいますが、そんなこと気にせずにメジャーを目指しましょう。",
        "カウントダウンTVだと最初のほうにチラッと入っている演歌みたいな順位です。更なる上を目指して芸風を変えてしまうのもいいかもしれません。",
        "ぶっちゃけ、ハシにも棒にもかからない、って感じの順位ですが、大事なのは伝えようとする気持ちです。これからもがんばってください。"
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
  },
  methods: {
    getRank: function(questions) {
      var score = 0;
      for (var i = 0; i < this.scoreList.length; i++) {
        score += this.scoreList[i][questions[`q${i + 2}`] - 1];
      }
      return 100 - score;
    },
    getDescription: function(questions) {
      var rank = this.getRank(questions);
      if (rank <= 10) {
        return this.descriptionList[0];
      } else if (rank <= 20) {
        return this.descriptionList[1];
      } else if (rank <= 30) {
        return this.descriptionList[2];
      } else if (rank <= 40) {
        return this.descriptionList[3];
      } else if (rank <= 50) {
        return this.descriptionList[4];
      } else if (rank > 50) {
        return this.descriptionList[5];
      } else {
        return -1;
      }
    },
    handleEnd() {
      console.log("end");
      this.$emit("end");
    }
  }
};
</script>

<style scoped>
.result {
  text-align: left;
}
.kansei {
  font-weight: bold;
}
</style>