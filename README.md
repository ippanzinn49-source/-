# -
鳴潮タイピング

<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>タイピングゲーム</title>
  <style>
    body {
      font-family: sans-serif;
      background: #101827;
      color: white;
      text-align: center;
      padding: 40px 16px;
    }
    .game {
      max-width: 600px;
      margin: auto;
      background: #202d42;
      padding: 28px;
      border-radius: 18px;
    }
    h1 { color: #7cffb2; }
    #word {
      font-size: 28px;
      margin: 30px 0;
      overflow-wrap: anywhere;
    }
    input {
      box-sizing: border-box;
      width: 100%;
      padding: 14px;
      font-size: 20px;
      border-radius: 8px;
      border: none;
    }
    button {
      padding: 12px 28px;
      margin: 12px;
      font-size: 17px;
      cursor: pointer;
      border: none;
      border-radius: 8px;
      background: #7cffb2;
    }
    .stats {
      display: flex;
      justify-content: space-around;
      gap: 12px;
    }
  </style>
</head>
<body>
  <div class="game">
    <h1>Typing Challenge</h1>

    <div class="stats">
      <p>残り時間：<span id="time">30</span>秒</p>
      <p>スコア：<span id="score">0</span></p>
    </div>

    <h2 id="word">スタートを押そう！</h2>

    <input id="input"
      type="text"
      placeholder="ここに入力..."
      autocomplete="off"
      disabled>

    <br>
    <button id="start">スタート</button>
    <p id="message">30秒間で何問正解できるかな？</p>
  </div>

  <script>
    const words = [
      "hello", "world", "typing", "computer",
      "javascript", "keyboard", "school",
      "programming", "game", "challenge",
      "apple", "orange", "beautiful", "friend"
    ];

    let currentWord = "";
    let score = 0;
    let time = 30;
    let timer = null;
    let playing = false;

    const wordEl = document.getElementById("word");
    const input = document.getElementById("input");
    const timeEl = document.getElementById("time");
    const scoreEl = document.getElementById("score");
    const message = document.getElementById("message");
    const startBtn = document.getElementById("start");

    function nextWord() {
      currentWord =
        words[Math.floor(Math.random() * words.length)];
      wordEl.textContent = currentWord;
      input.value = "";
    }

    function startGame() {
      clearInterval(timer);

      score = 0;
      time = 30;
      playing = true;

      scoreEl.textContent = score;
      timeEl.textContent = time;
      message.textContent = "ゲーム開始！";
      input.disabled = false;
      startBtn.disabled = true;
      input.focus();

      nextWord();

      timer = setInterval(() => {
        time--;
        timeEl.textContent = time;

        if (time <= 0) {
          clearInterval(timer);
          playing = false;
          input.disabled = true;
          startBtn.disabled = false;
          wordEl.textContent = "終了！";
          message.textContent =
            `最終スコア：${score}点！`;
        }
      }, 1000);
    }

    input.addEventListener("input", () => {
      if (!playing) return;

      if (input.value.trim() === currentWord) {
        score++;
        scoreEl.textContent = score;
        message.textContent = "正解！";
        nextWord();
      }
    });

    startBtn.addEventListener("click", startGame);
  </script>
</body>
</html>
