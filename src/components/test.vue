<template>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>隨機字母猜測遊戲</title>
</head>

  <!-- <div class="grid-container" id="gridContainer"></div> -->

  <div>{{ test2 }}</div>
  <div class="button-container">
    <button @click="checkAnswer">確認</button>
    <button @click="showHint">提示</button>
    <button @click="playAudio">語音</button>
  </div>

  <div class="result">
    <span id="correctCount">答對: 0</span>
    <span id="incorrectCount">答錯: 0</span>
  </div>

</template>

<script>
    //const randomCount = Math.floor(Math.random() * 5) + 3; // 隨機生成3到7個格子
    const randomCount = 5;
    const answers = [];
    const userInputs = [];
    let correctCount = 0;
    let incorrectCount = 0;

    


    // 隨機生成格子
    function generateGrid() {
    // const gridContainer = document.getElementsByClassName("grid-container");
    // const gridContainer = document.getElementById("gridContainer");
    //   gridContainer.innerHTML = '';

      for (let i = 0; i < randomCount; i++) {
        const letter = String.fromCharCode(65 + Math.floor(Math.random() * 26)); // 隨機字母 A-Z
        answers.push(letter);

        const input = document.createElement('input');
        input.type = 'text';
        input.maxLength = 1;
        input.className = 'input-box';
        input.addEventListener('input', (event) => {
          userInputs[i] = event.target.value.toUpperCase();
        });

        // gridContainer.appendChild(input);
      }
    }

    // 確認答案
    function checkAnswer() {
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
    }

    // 提示功能
    function showHint() {
      alert(`答案是: ${answers.join(', ')}`);
    }

    // 語音播放功能 (可自訂為各個格子的字母發音)
    function playAudio() {
      const speech = new SpeechSynthesisUtterance(`Letters are ${answers.join(', ')}`);
      speech.lang = 'en-US';
      window.speechSynthesis.speak(speech);
    }

    // 初始化
    generateGrid();
</script>

<style>
body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
  font-family: Arial, sans-serif;
}

.grid-container {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
}

.input-box {
  width: 50px;
  height: 50px;
  text-align: center;
  font-size: 24px;
}

.button-container {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}

.result {
  font-size: 18px;
  margin-top: 20px;
}
</style>