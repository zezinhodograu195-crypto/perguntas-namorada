# perguntas-namorada
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Perguntas ❤️</title>
  <style>
    body {
      margin: 0;
      background-color: black;
      color: white;
      font-family: 'Poppins', sans-serif;
      text-align: center;
      overflow: hidden;
    }

    /* corações animados */
    .heart {
      position: fixed;
      color: red;
      font-size: 24px;
      animation: floatUp 6s linear infinite;
      opacity: 0.8;
    }
    @keyframes floatUp {
      0% { transform: translateY(100vh) scale(1); opacity: 1; }
      100% { transform: translateY(-10vh) scale(0.5); opacity: 0; }
    }

    h1 {
      margin-top: 60px;
      color: #ff2444;
      font-size: 2.2em;
    }

    .question {
      display: none;
      margin-top: 40px;
    }

    button {
      background-color: #ff2444;
      color: white;
      border: none;
      padding: 12px 18px;
      margin: 10px;
      border-radius: 10px;
      font-size: 18px;
      cursor: pointer;
      transition: transform 0.2s;
    }

    button:hover {
      transform: scale(1.05);
    }

    #tapToPlay {
      position: fixed;
      inset: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      background: rgba(0, 0, 0, 0.8);
      z-index: 999;
    }

    #finalMessage {
      display: none;
      font-size: 24px;
      margin-top: 40px;
      color: #ffccdd;
    }

    #loveSection {
      display: none;
      margin-top: 30px;
    }

    #progressText {
      margin-top: 20px;
      font-size: 24px;
      color: #ffdd00;
    }

    #restartBtn {
      display: none;
      background-color: #ff5fa2;
      color: white;
      font-size: 18px;
      padding: 12px 25px;
      border: none;
      border-radius: 10px;
      margin-top: 30px;
      cursor: pointer;
      transition: transform 0.2s;
    }

    #restartBtn:hover {
      transform: scale(1.05);
    }
  </style>
</head>
<body>

  <!-- Música -->
  <div id="tapToPlay">
    <button id="startBtn">Toque para começar ❤️</button>
  </div>
  <audio id="bgMusic" loop playsinline>
    <source src="nuts.mp3" type="audio/mpeg">
  </audio>

  <h1>Perguntas 💖</h1>

  <!-- Perguntas -->
  <div id="q1" class="question">
    <h2>1️⃣ Qual o nome da nossa futura filha?</h2>
    <button onclick="checkAnswer(1, 'Antonieta')">Antonieta</button>
    <button onclick="checkAnswer(1, 'Angela')">Angela</button>
    <button onclick="checkAnswer(1, 'Piastra')">Piastra</button>
    <button onclick="checkAnswer(1, 'Sofia')">Sofia</button>
  </div>

  <div id="q2" class="question">
    <h2>2️⃣ Quando nós iremos fazer 6 meses de namoro?</h2>
    <button onclick="checkAnswer(2, 'Janeiro')">Janeiro</button>
    <button onclick="checkAnswer(2, 'Março')">Março</button>
    <button onclick="checkAnswer(2, 'Fevereiro')">Fevereiro</button>
    <button onclick="checkAnswer(2, 'Abril')">Abril</button>
  </div>

  <div id="q3" class="question">
    <h2>3️⃣ Quem disse "eu te amo" primeiro?</h2>
    <button onclick="checkAnswer(3, 'Eu')">Eu</button>
    <button onclick="checkAnswer(3, 'Você')">Você</button>
  </div>

  <div id="q4" class="question">
    <h2>4️⃣ Quando foi a primeira vez que eu te disse que te amava?</h2>
    <button onclick="checkAnswer(4, '02/09/2025')">02/09/2025</button>
    <button onclick="checkAnswer(4, '21/08/2025')">21/08/2025</button>
    <button onclick="checkAnswer(4, '25/08/2025')">25/08/2025</button>
    <button onclick="checkAnswer(4, '01/09/2025')">01/09/2025</button>
  </div>

  <div id="q5" class="question">
    <h2>5️⃣ O que você mais ama em mim?</h2>
    <input type="text" id="answer5" placeholder="Escreva sua resposta..." style="padding:10px;border-radius:8px;width:60%;font-size:16px;">
    <br><br>
    <button onclick="finishQuiz()">Enviar 💌</button>
  </div>

  <!-- Mensagem final -->
  <div id="finalMessage">🎉 Parabéns! Você terminou ❤️🎉</div>

  <!-- Botão interativo de amor -->
  <div id="loveSection">
    <button id="loveButton">Quanto você me ama? Clique aqui 👇🏻</button>
    <div id="progressText">0%</div>
  </div>

  <!-- Botão de recomeçar -->
  <button id="restartBtn" onclick="restart()">Recomeçar 💞</button>

  <script>
    const bg = document.getElementById('bgMusic');
    document.getElementById('startBtn').addEventListener('click', () => {
      bg.play().catch(()=>{});
      document.getElementById('tapToPlay').style.display = 'none';
      startHearts();
      showQuestion(1);
    });

    const correctAnswers = {
      1: 'Antonieta',
      2: 'Março',
      3: 'Você',
      4: '21/08/2025'
    };

    let currentQuestion = 1;

    function showQuestion(num) {
      document.querySelectorAll('.question').forEach(q => q.style.display = 'none');
      const el = document.getElementById('q' + num);
      if (el) el.style.display = 'block';
    }

    function checkAnswer(num, answer) {
      if (answer === correctAnswers[num]) {
        alert('Acertou minha princesa 🥳🥳');
        currentQuestion++;
        if (currentQuestion <= 5) {
          showQuestion(currentQuestion);
        } else {
          showFinal();
        }
      } else {
        alert('Errou minha linda 😢');
      }
    }

    function finishQuiz() {
      showFinal();
    }

    function showFinal() {
      document.querySelectorAll('.question').forEach(q => q.style.display = 'none');
      document.getElementById('finalMessage').style.display = 'block';
      document.getElementById('loveSection').style.display = 'block';
      document.getElementById('restartBtn').style.display = 'inline-block';
    }

    // Botão de amor
    let loveClicks = 0;
    const totalClicks = 5;
    const progressText = document.getElementById('progressText');
    const loveButton = document.getElementById('loveButton');

    loveButton.addEventListener('click', () => {
      loveClicks++;
      let percent = Math.min((loveClicks / totalClicks) * 100, 100);
      progressText.textContent = `${percent}%`;
      if (loveClicks >= totalClicks) {
        loveButton.disabled = true;
        loveButton.textContent = "❤️ 100% completo ❤️";
      }
    });

    // Recomeçar
    function restart() {
      loveClicks = 0;
      loveButton.disabled = false;
      loveButton.textContent = "Quanto você me ama? Clique aqui 👇🏻";
      progressText.textContent = "0%";
      currentQuestion = 1;
      document.getElementById('finalMessage').style.display = 'none';
      document.getElementById('loveSection').style.display = 'none';
      document.getElementById('restartBtn').style.display = 'none';
      showQuestion(1);
    }

    // Corações flutuantes
    function startHearts() {
      setInterval(() => {
        const heart = document.createElement('div');
        heart.classList.add('heart');
        heart.style.left = Math.random() * 100 + 'vw';
        heart.style.fontSize = Math.random() * 20 + 20 + 'px';
        heart.textContent = '❤️';
        document.body.appendChild(heart);
        setTimeout(() => heart.remove(), 6000);
      }, 400);
    }
  </script>
</body>
</html>
index.html
