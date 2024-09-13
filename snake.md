---
layout: blank
title: Snake Game
permalink: /snake
---
<a href="/alex_2025/">Home</a>

<style>
  html, body {
    height: 100%;
    margin: 0;
    overflow: hidden; /* Prevent scrolling */
  }
  canvas {
    display: block;
    margin: auto;
    border: 1px solid #000;
    background-color: #fff;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
</style>

<canvas id="gameCanvas" width="400" height="400"></canvas>

<script>
  const canvas = document.getElementById('gameCanvas');
  const ctx = canvas.getContext('2d');
  const scale = 20;
  const rows = canvas.height / scale;
  const columns = canvas.width / scale;

  let snake = [{ x: 10, y: 10 }];
  let food = { x: 15, y: 15 };
  let dx = scale;
  let dy = 0;
  let score = 0;

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    drawSnake();
    drawFood();
    moveSnake();
    checkCollision();
    checkFoodCollision();
  }

  function drawSnake() {
    ctx.fillStyle = 'green';
    for (let segment of snake) {
      ctx.fillRect(segment.x * scale, segment.y * scale, scale, scale);
    }
  }

  function drawFood() {
    ctx.fillStyle = 'red';
    ctx.fillRect(food.x * scale, food.y * scale, scale, scale);
  }

  function moveSnake() {
    const head = { x: snake[0].x + dx / scale, y: snake[0].y + dy / scale };
    snake.unshift(head);
    snake.pop();
  }

  function checkCollision() {
    const head = snake[0];
    // Check wall collisions
    if (head.x < 0 || head.x >= columns || head.y < 0 || head.y >= rows) {
      resetGame();
    }
    // Check self collisions
    for (let i = 1; i < snake.length; i++) {
      if (head.x === snake[i].x && head.y === snake[i].y) {
        resetGame();
      }
    }
  }

  function checkFoodCollision() {
    const head = snake[0];
    if (head.x === food.x && head.y === food.y) {
      snake.push({ ...snake[snake.length - 1] });
      score++;
      spawnFood();
    }
  }

  function spawnFood() {
    food = {
      x: Math.floor(Math.random() * columns),
      y: Math.floor(Math.random() * rows),
    };
  }

  function resetGame() {
    snake = [{ x: 10, y: 10 }];
    dx = scale;
    dy = 0;
    score = 0;
    spawnFood();
  }

  function handleKeyPress(e) {
    e.preventDefault();
    switch (e.key) {
      case 'ArrowUp':
        if (dy === 0) { dx = 0; dy = -scale; }
        break;
      case 'ArrowDown':
        if (dy === 0) { dx = 0; dy = scale; }
        break;
      case 'ArrowLeft':
        if (dx === 0) { dx = -scale; dy = 0; }
        break;
      case 'ArrowRight':
        if (dx === 0) { dx = scale; dy = 0; }
        break;
    }
  }

  document.addEventListener('keydown', handleKeyPress);

  setInterval(draw, 100);
</script>


