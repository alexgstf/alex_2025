---
layout: base
title: Snake Game
permalink: /games/snake
---

{% include nav/mainnav.html %}

<div id="snake-game" style="width: 400px; height: 400px; border: 2px solid #333; position: relative; margin: auto;">
    <canvas id="gameCanvas" width="400" height="400" style="background-color: #f0f0f0;"></canvas>
    <div id="score" style="text-align: center; margin-top: 10px; color: white;">Score: 0</div>
</div>

<script>
    const canvas = document.getElementById("gameCanvas");
    const ctx = canvas.getContext("2d");
    const box = 20;
    let score = 0;
    let game;

    let snake, food, d;

    document.addEventListener("keydown", direction);
    startGame();

    function startGame() {
        score = 0;
        d = null; // Reset direction
        snake = [{ x: box * 5, y: box * 5 }];
        food = { x: Math.floor(Math.random() * 20) * box, y: Math.floor(Math.random() * 20) * box };
        document.getElementById("score").innerText = "Score: 0";
        game = setInterval(draw, 100);
    }

    function direction(event) {
        event.preventDefault(); // Prevent default behavior (scrolling)
        if (event.keyCode === 37 && d !== "RIGHT") d = "LEFT";
        else if (event.keyCode === 38 && d !== "DOWN") d = "UP";
        else if (event.keyCode === 39 && d !== "LEFT") d = "RIGHT";
        else if (event.keyCode === 40 && d !== "UP") d = "DOWN";
    }

    function collision(head, array) {
        for (let i = 0; i < array.length; i++) {
            if (head.x === array[i].x && head.y === array[i].y) {
                return true;
            }
        }
        return false;
    }

    function draw() {
        ctx.fillStyle = "#f0f0f0";
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        for (let i = 0; i < snake.length; i++) {
            ctx.fillStyle = (i === 0) ? "green" : "lightgreen";
            ctx.fillRect(snake[i].x, snake[i].y, box, box);
            ctx.strokeStyle = "darkgreen";
            ctx.strokeRect(snake[i].x, snake[i].y, box, box);
        }

        ctx.fillStyle = "red";
        ctx.fillRect(food.x, food.y, box, box);

        let snakeX = snake[0].x;
        let snakeY = snake[0].y;

        if (d === "LEFT") snakeX -= box;
        if (d === "UP") snakeY -= box;
        if (d === "RIGHT") snakeX += box;
        if (d === "DOWN") snakeY += box;

        if (snakeX === food.x && snakeY === food.y) {
            score++;
            food = { x: Math.floor(Math.random() * 20) * box, y: Math.floor(Math.random() * 20) * box };
        } else {
            snake.pop();
        }

        let newHead = { x: snakeX, y: snakeY };

        if (snakeX < 0 || snakeY < 0 || snakeX >= canvas.width || snakeY >= canvas.height || collision(newHead, snake)) {
            clearInterval(game);
            alert("Game Over! Your score: " + score);
            startGame(); // Restart the game automatically
            return;
        }

        snake.unshift(newHead);
        document.getElementById("score").innerText = "Score: " + score;
    }
</script>
