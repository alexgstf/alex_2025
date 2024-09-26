---
layout: base
title: "Number Guessing Game"
permalink: /games/ng
---

{% include nav/games.html %}

<div id="game">
  <h2>Guess the Number!</h2>
  <p>Pick a number between 1 and 100.</p>
  <input type="number" id="guessInput" min="1" max="100" />
  <button id="guessButton">Guess</button>
  <p id="result"></p>
  <p>Attempts: <span id="attempts">0</span></p>
  <button id="restartButton" style="display:none;">Restart Game</button>
</div>

<script>
  let targetNumber = Math.floor(Math.random() * 100) + 1;
  let attempts = 0;

  document.getElementById('guessButton').onclick = function() {
    const guess = Number(document.getElementById('guessInput').value);
    attempts++;
    document.getElementById('attempts').innerText = attempts;

    if (guess < 1 || guess > 100) {
      document.getElementById('result').innerText = 'Please enter a number between 1 and 100.';
    } else if (guess < targetNumber) {
      document.getElementById('result').innerText = 'Too low! Try again.';
    } else if (guess > targetNumber) {
      document.getElementById('result').innerText = 'Too high! Try again.';
    } else {
      document.getElementById('result').innerText = `Congratulations! You've guessed the number ${targetNumber} in ${attempts} attempts.`;
      document.getElementById('restartButton').style.display = 'block';
    }
  };

  document.getElementById('restartButton').onclick = function() {
    targetNumber = Math.floor(Math.random() * 100) + 1;
    attempts = 0;
    document.getElementById('attempts').innerText = attempts;
    document.getElementById('result').innerText = '';
    document.getElementById('restartButton').style.display = 'none';
    document.getElementById('guessInput').value = '';
  };
</script>
