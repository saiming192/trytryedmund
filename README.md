<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>夾公仔機小遊戲</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: #f1f1f1;
      overflow: hidden;
      font-family: sans-serif;
      user-select: none;
    }

    #game {
      position: relative;
      width: 100vw;
      height: 100vh;
      background: #d0eaff;
      overflow: hidden;
    }

    #claw {
      position: absolute;
      width: 60px;
      height: 60px;
      background: gray;
      border-radius: 50%;
      top: 50px;
      left: 50px;
      z-index: 10;
    }

    .doll {
      position: absolute;
      width: 50px;
      height: 50px;
      background-image: url('https://i.imgur.com/5Z3mI6o.png'); /* 示意圖：可換 Chiikawa */
      background-size: cover;
    }

    #hole {
      position: absolute;
      width: 80px;
      height: 40px;
      background: black;
      bottom: 20px;
      left: 20px;
      border-radius: 50% / 100%;
      z-index: 1;
    }

    #startBtn {
      position: absolute;
      top: 20px;
      right: 20px;
      padding: 10px 20px;
      background: #f39c12;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }

    #timer {
      position: absolute;
      top: 20px;
      left: 20px;
      font-size: 20px;
    }
  </style>
</head>
<body>
  <div id="game">
    <div id="claw"></div>
    <div id="hole"></div>
    <div class="doll" style="left: 300px; bottom: 50px;"></div>
    <div class="doll" style="left: 400px; bottom: 50px;"></div>
    <div id="timer">倒數：10</div>
    <button id="startBtn">開始</button>
  </div>

  <script>
    const claw = document.getElementById('claw');
    const dolls = document.querySelectorAll('.doll');
    const startBtn = document.getElementById('startBtn');
    const timerDisplay = document.getElementById('timer');

    let moving = false;
    let timer = 10;
    let interval;
    let clawSpeed = 10;

    let forceType = 'weak'; // 預設弱力

    function getRandomForce() {
      const rand = Math.floor(Math.random() * 10);
      if (rand === 0) return 'strong';
      if (rand === 1) return 'medium';
      return 'weak';
    }

    function moveClaw(e) {
      if (!moving) return;
      const rect = claw.getBoundingClientRect();
      let left = claw.offsetLeft;
      let top = claw.offsetTop;
      if (e.key === 'ArrowLeft') left -= clawSpeed;
      if (e.key === 'ArrowRight') left += clawSpeed;
      if (e.key === 'ArrowUp') top -= clawSpeed;
      if (e.key === 'ArrowDown') top += clawSpeed;

      claw.style.left = `${Math.max(0, Math.min(window.innerWidth - 60, left))}px`;
      claw.style.top = `${Math.max(0, Math.min(window.innerHeight - 60, top))}px`;
    }

    function dropClaw() {
      moving = false;
      document.removeEventListener('keydown', moveClaw);
      const clawRect = claw.getBoundingClientRect();
      const holeRect = document.getElementById('hole').getBoundingClientRect();

      let grabbed = false;

      dolls.forEach(doll => {
        const dollRect = doll.getBoundingClientRect();
        const isOverlap = !(clawRect.right < dollRect.left ||
                            clawRect.left > dollRect.right ||
                            clawRect.bottom < dollRect.top ||
                            clawRect.top > dollRect.bottom);
        if (isOverlap) {
          const force = getRandomForce();
          forceType = force;
          if (force === 'strong') {
            doll.style.transition = '1s';
            doll.style.left = holeRect.left + 'px';
            doll.style.bottom = '20px';
            grabbed = true;
          } else if (force === 'medium') {
            // 50% 成功
            if (Math.random() < 0.5) {
              doll.style.transition = '1s';
              doll.style.left = holeRect.left + 'px';
              doll.style.bottom = '20px';
              grabbed = true;
            }
          }
        }
      });

      if (!grabbed) {
        alert('夾不到或公仔滑掉了！（爪力：' + forceType + '）');
      }
    }

    function startGame() {
      timer = 10;
      timerDisplay.innerText = `倒數：${timer}`;
      moving = true;
      forceType = 'weak';
      document.addEventListener('keydown', moveClaw);

      interval = setInterval(() => {
        timer--;
        timerDisplay.innerText = `倒數：${timer}`;
        if (timer <= 0) {
          clearInterval(interval);
          dropClaw();
        }
      }, 1000);
    }

    startBtn.addEventListener('click', startGame);
  </script>
</body>
</html>
