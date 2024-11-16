<template>

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>隨機字母猜測遊戲</title>
  </head>
  <div class="content">
    <div class="wrap">
      <!-- <div v-html="gridContainer"></div> -->
      <input v-for="item in randomCount" type="text" class="box" maxlength="1" autocapitalize="off" autocomplete="off"
        v-bind:id="i"></input>
    </div>
    <div class="button-container">
      <button @click="checkAnswer">確認</button>
      <button @click="showHint">提示</button>
      <button @click="playAudio">語音</button>
    </div>

    <div class="result">
      <span id="correctCount">答對: 0</span>
      <span id="incorrectCount">答錯: 0</span>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      randomCount: 5,
      answerWord: 'apple',
      answers: [],
      userInputs: [],
      gridContainer: this.generateGrid(),
      correctCount: 0,
      incorrectCount: 0,
    }
  },
  methods: {
    // 隨機生成格子
    generateGrid: function () {
      let box = ''
      for (let i = 0; i < this.randomCount; i++) {
        var letter = String.fromCharCode(65 + Math.floor(Math.random() * 26)); // 隨機字母 A-Z
        this.answers.push(letter);
        box += '<input type="text" class="box" maxlength="1" autocapitalize="off" autocomplete="off" v-bind:id="i">"&nbsp"';
      }
      return box;
    },

    // 確認答案
    checkAnswer: function () {
      correctCount = 0;
      incorrectCount = 0;

      answers.forEach((answer, index) => {
        if (userInputs[index] === answer) {
          correctCount++;
        } else {
          incorrectCount++;
        }
      });

      document.getElementById('correctCount').textContent = `答對: ${correctCount}`;
      document.getElementById('incorrectCount').textContent = `答錯: ${incorrectCount}`;
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
  }
}

//const randomCount = Math.floor(Math.random() * 5) + 3; // 隨機生成3到7個格子
</script>

<style>
main {
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
}
</style>