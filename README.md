<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Whack-a-Mole Game</title>
  <style>
    /* You can add CSS styling here */
    /* For example, customize the appearance of the game elements */
    .container {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
      margin-top: 20px;
    }
    .hole {
      width: 100px;
      height: 100px;
      background: #9c7248;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 24px;
      cursor: pointer;
      transition: background 0.3s;
    }
    .hole.active {
      background: #c7a06b;
    }
  </style>
</head>
<body>

<h1>Whack-a-Mole Game</h1>

<div class="container">
  <div class="hole"></div>
  <div class="hole"></div>
  <div class="hole"></div>
  <div class="hole"></div>
  <div class="hole"></div>
  <div class="hole"></div>
  <div class="hole"></div>
  <div class="hole"></div>
  <div class="hole"></div>
</div>

<script>
  // JavaScript for the game logic
  const holes = document.querySelectorAll('.hole');
  let score = 0;

  function randomTime(min, max) {
    return Math.round(Math.random() * (max - min) + min);
  }

  function randomHole() {
    const idx = Math.floor(Math.random() * holes.length);
    const hole = holes[idx];
    return hole;
  }

  function peep() {
    const time = randomTime(200, 1000);
    const hole = randomHole();
    hole.classList.add('active');
    setTimeout(() => {
      hole.classList.remove('active');
      if (!gameOver) peep();
    }, time);
  }

  holes.forEach(hole => hole.addEventListener('click', bonk));

  function bonk(e) {
    if (!e.isTrusted) return; // Prevent cheating by automated clicking
    score++;
    this.classList.remove('active');
  }

  let gameOver = false;
  setTimeout(() => {
    gameOver = true;
    alert(`Game Over! Your final score is ${score}.`);
  }, 10000); // Game duration (in milliseconds)

  peep(); // Start the game
</script>

</body>
</html>
