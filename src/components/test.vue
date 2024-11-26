<template>

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>隨機字母猜測遊戲</title>
  </head>
  <div class="content">
    <div class="wrap">
      <input v-for="(item, index) in answer" type="text" class="box" maxlength="1" autocapitalize="off"
        autocomplete="off" v-bind:id="index"></input>
    </div>
    <div class="hint"></div>
    <div class="button-container">
      <button @click="checkAnswer">確認</button>
      <button @click="showHint">提示</button>
      <button @click="playAudio">語音</button>
    </div>

    <div class="result">
      <span id="correctCount">答對: {{ correctCount }}</span>
      <span id="incorrectCount">答錯: {{ incorrectCount }}</span>
    </div>
  </div>
</template>

<script>


export default {

  data() {
    return {
      correctCount: 0,
      incorrectCount: 0,
      answer: [],
      problem: {},
      problems: [
        { word: "apple", hint: "a" },
        { word: "banana", hint: "b" },
        { word: "cow", hint: "c" }
      ],
    }
  },
  methods: {
    generateGrid: function () {
      this.problem = this.problems[Math.floor(Math.random() * (this.problems.length))];
      console.log(this.problem)
      this.answer = this.problem.word.split('');
      console.log(this.answer)

    },

    // 確認答案
    checkAnswer: function () {
      // correctCount = 0;
      // incorrectCount = 0;

      for (let i = 0; i < this.answer.length; i++) {
        // console.log('-------------')
        // console.log($(`#${i}`).val())

        $(`#${i}`).val($(`#${i}`).val().toLowerCase())
        console.log($(`#${i}`).val().toLowerCase())

        if ($(`#${i}`).val() != this.answer[i]) {
          this.incorrectCount += 1;
          alert('Wrong answer!')
          return
        }

      }
      this.correctCount += 1;
      for(let i = 0; i < this.answer.length; i++){
        $(`#${i}`).val('')
      }

      this.generateGrid()
    },

    // 提示功能
    showHint: function () {
      alert(`答案是: ${answers.join(', ')}`);
    },

    // 語音播放功能 (可自訂為各個格子的字母發音)
    playAudio: function () {
      const speech = new SpeechSynthesisUtterance(`Letters are ${answers.join(', ')}`);
      speech.lang = 'en-US';
      window.speechSynthesis.speak(speech);
    },
  },
  mounted() {
    this.generateGrid()
  }
}

//const randomCount = Math.floor(Math.random() * 5) + 3; // 隨機生成3到7個格子
</script>

<style>
.content {
  text-align: center;
  width: 100%;
  align-items: center;
  position: absolute;
  top: 30%;
}

.box {
  margin: 0 5px;
  width: 30px;
  height: 40px;
}

.wrap {
  width: 80%;
  display: flex;
  flex-wrap: nowrap;
  justify-content: center;
  gap: 15px;
  margin: auto;
  margin-bottom: 50px;
}

.result {
  display: flex;
  justify-content: space-around;
}

button {
  height: 40px;
  width: 80px;
}

/* main {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  text-align: center;
}

.content {
  text-align: center;
  height: 100vh;
  margin: auto;
  padding-top: 30vh;
}

.box {
  margin: 0 5px;
  height: 40px;
}

button {
  height: 40px;
  width: 80px;
} */
</style>