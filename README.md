!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>圖案移動小遊戲</title>
  <style>
    #game {
      width: 500px;
      height: 200px;
      border: 2px solid #000;
      position: relative;
    }
    #player {
      width: 50px;
      height: 50px;
      background-color: red;
      position: absolute;
      top: 75px;
      left: 0;
    }
  </style>
</head>
<body>
  <h2>按左鍵讓圖案向左移動！</h2>
  <div id="game">
    <div id="player"></div>
  </div>
  <button onclick="moveLeft()">← 左移</button>

  <script>
    let player = document.getElementById("player");
    let position = 0;

    function moveLeft() {
      position -= 20;  // 每次向左移動 20px
      if (position < 0) position = 0;  // 不讓超出邊界
      player.style.left = position + "px";
    }
  </script>
</body>
</html>
