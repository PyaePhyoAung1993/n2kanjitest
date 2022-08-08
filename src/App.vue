<template>
  <div class="ctr">
    <h1>N2 Kanji Test</h1>
    <questions
      v-if="questionsAnswered < questions.length"
      :questions="questions"
      :questionsAnswered="questionsAnswered"
      @question-answered="questionAnswered"
    ></questions>

    <result
      :questions="questions"
      v-else
      :results="results"
      :totalCorrect="totalCorrect"
    ></result>
    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import Questions from "./components/Questions.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: "1. 語義だけでなく、内容についてさまざまな（　角度　）から調べ、理解することが必要です。",
          answers: [
            {
              text: "１．かくど",
              is_correct: true,
            },
            {
              text: "２．かくたび",
              is_correct: false,
            },
            {
              text: "３．すみど",
              is_correct: false,
            },
            {
              text: "４．すみたび",
              is_correct: false,
            },
          ],
        },
        {
          q: "2. 大原さんは、検診で「問題なし」とされた半年後に体調を壊し、病院でがんと（　しんだん　））され１年で亡くなりました。",
          answers: [
            {
              text: "１． 診断",
              is_correct: true,
            },
            {
              text: "２．珍断",
              is_correct: false,
            },
            {
              text: "３．修断",
              is_correct: false,
            },
            {
              text: "４．惨断",
              is_correct: false,
            },
          ],
        },
        {
          q: "3. あるキーワードで検索すると、古い記事ばかりヒットしてしまい、有益な情報が得られないということも少なくない。そんな場合は、期間を（　指定　）して検索してみよう。",
          answers: [
            {
              text: "１．じてい",
              is_correct: false,
            },
            {
              text: "２．じってい",
              is_correct: false,
            },
            {
              text: "３．してい",
              is_correct: true,
            },
            {
              text: "４．しってい",
              is_correct: false,
            },
          ],
        },
        {
          q: "4. 遺伝子レベルでがんの可能性を発見して、経過観察も含めた治療を開始して（　とうけい　）をとれば、１０年生存率も飛躍的に上がります。その治療に意味があるかは言うまでもありません。",
          answers: [
            {
              text: "１．結計",
              is_correct: false,
            },
            {
              text: "２．絡計",
              is_correct: false,
            },
            {
              text: "３．絞計",
              is_correct: false,
            },
            {
              text: "４．統計",
              is_correct: true,
            },
          ],
        },
        {
          q: "5. 天気予報によれば、来週の日本（　列島　）は、全国的に晴天が続くそうです。",
          answers: [
            {
              text: "１．れいしま",
              is_correct: false,
            },
            {
              text: "２．れっとう",
              is_correct: true,
            },
            {
              text: "３．れいとう",
              is_correct: false,
            },
            {
              text: "４．れっしま",
              is_correct: true,
            },
          ],
        },
        {
          q: "6. 天気予報によれば、来週の日本列島は、全国的に（　晴天　））が続くそうです。",
          answers: [
            {
              text: "１．せいてん",
              is_correct: true,
            },
            {
              text: "２．せいでん",
              is_correct: false,
            },
            {
              text: "３．すいてん",
              is_correct: false,
            },
            {
              text: "４．すいでん",
              is_correct: true,
            },
          ],
        },
        {
          q: "7. それから二ヵ月後、北朝鮮は地下核実験を行い、１９５３の休戦協定には（　縛られない　））と宣言した。",
          answers: [
            {
              text: "１．しぼられない",
              is_correct: false,
            },
            {
              text: "２．しばられない",
              is_correct: true,
            },
            {
              text: "３．せぼられない",
              is_correct: false,
            },
            {
              text: "４．せばられない",
              is_correct: true,
            },
          ],
        },
        {
          q: "8. 数ヶ月前、仕上げた（　げんこう ）を渡したときに編集者の顔に浮かんだ表情も、いまのあなたと同じだ。",
          answers: [
            {
              text: "１．原稿",
              is_correct: true,
            },
            {
              text: "２．願稿",
              is_correct: false,
            },
            {
              text: "３．原橋",
              is_correct: false,
            },
            {
              text: "４．願橋",
              is_correct: true,
            },
          ],
        },
        {
          q: "9. アユミは部屋のむこうにある鏡の前まで行くと、なめらかな髪の毛をうっとりと（　撫でた　））。",
          answers: [
            {
              text: "１．はでた",
              is_correct: false,
            },
            {
              text: "２．なでた",
              is_correct: true,
            },
            {
              text: "３．いでた",
              is_correct: false,
            },
            {
              text: "４．ゆでた",
              is_correct: true,
            },
          ],
        },
        {
          q: "10. 荷物の（　じゅうりょう　））が２０キロをちょうかした場合は、ついか料金をせいきゅうされます。",
          answers: [
            {
              text: "１．重料",
              is_correct: false,
            },
            {
              text: "２．集両",
              is_correct: false,
            },
            {
              text: "３．重量",
              is_correct: true,
            },
            {
              text: "４．銃量",
              is_correct: true,
            },
          ],
        },
        {
          q: "11. 荷物のじゅうりょうが２０キロを（　ちょうか　））した場合は、ついか料金をせいきゅうされます。",
          answers: [
            {
              text: "１．越過",
              is_correct: false,
            },
            {
              text: "２．超課",
              is_correct: false,
            },
            {
              text: "３．越課",
              is_correct: false,
            },
            {
              text: "４．超過",
              is_correct: true,
            },
          ],
        },
        {
          q: "12. 荷物のじゅうりょうが２０キロをちょうかした場合は、（　ついか　））料金をせいきゅうされます。",
          answers: [
            {
              text: "１．追加",
              is_correct: true,
            },
            {
              text: "２．堆加",
              is_correct: false,
            },
            {
              text: "３．追価",
              is_correct: false,
            },
            {
              text: "４．堆価",
              is_correct: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!",
        },
        {
          min: 12,
          max: 12,
          title: "Wow, you're a genius!",
          desc: "Congratulation! You are strong in Kanji",
        },
      ],
    };
  },
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }
      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>


