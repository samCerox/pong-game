<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Pong Game</title>
<style>
    canvas {
        border: 1px solid black;
        display: block;
        margin: 0 auto;
    }
    #scoreboard {
        text-align: center;
        font-size: 24px;
    }
    #controls {
        text-align: center;
        margin-top: 20px;
    }
</style>
</head>
<body>

<h1 style="text-align:center;">Pong Game</h1>

<div id="scoreboard">
    Player 1: <span id="player1Score">0</span> |
    Player 2: <span id="player2Score">0</span>
</div>

<canvas id="gameCanvas" width="600" height="400"></canvas>

<div id="controls">
    <button id="startButton">Start Game</button>
    <button id="resetButton">Reset Game</button>
</div>

<p style="text-align:center;">
Player 1: W / S <br>
Player 2: ↑ / ↓
</p>

<script>
let player1Score = 0;
let player2Score = 0;

const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

const paddleHeight = 80;
const paddleWidth = 10;

let player1Y = 160;
let player2Y = 160;

let ballX = 300;
let ballY = 200;
let ballSpeedX = 4;
let ballSpeedY = 4;

let gameRunning = false;

// Controles
const keys = {};

document.addEventListener('keydown', (e) => keys[e.key] = true);
document.addEventListener('keyup', (e) => keys[e.key] = false);

document.getElementById('startButton').addEventListener('click', () => {
    if (!gameRunning) {
        gameRunning = true;
        gameLoop();
    }
});

document.getElementById('resetButton').addEventListener('click', resetGame);

function resetGame() {
    player1Score = 0;
    player2Score = 0;
    ballX = 300;
    ballY = 200;
    updateScoreboard();
}

function updateScoreboard() {
    document.getElementById('player1Score').innerText = player1Score;
    document.getElementById('player2Score').innerText = player2Score;
}

function movePaddles() {
    if (keys['w'] && player1Y > 0) player1Y -= 5;
    if (keys['s'] && player1Y < canvas.height - paddleHeight) player1Y += 5;

    if (keys['ArrowUp'] && player2Y > 0) player2Y -= 5;
    if (keys['ArrowDown'] && player2Y < canvas.height - paddleHeight) player2Y += 5;
}

function moveBall() {
    ballX += ballSpeedX;
    ballY += ballSpeedY;

    // Rebote arriba/abajo
    if (ballY <= 0 || ballY >= canvas.height) {
        ballSpeedY *= -1;
    }

    // Colisión con paletas
    if (ballX <= 20 && ballY > player1Y && ballY < player1Y + paddleHeight) {
        ballSpeedX *= -1;
    }

    if (ballX >= canvas.width - 20 && ballY > player2Y && ballY < player2Y + paddleHeight) {
        ballSpeedX *= -1;
    }

    // Punto
    if (ballX <= 0) {
        player2Score++;
        resetBall();
    }

    if (ballX >= canvas.width) {
        player1Score++;
        resetBall();
    }

    updateScoreboard();
}

function resetBall() {
    ballX = canvas.width / 2;
    ballY = canvas.height / 2;
    ballSpeedX *= -1;
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // Paletas
    ctx.fillRect(10, player1Y, paddleWidth, paddleHeight);
    ctx.fillRect(canvas.width - 20, player2Y, paddleWidth, paddleHeight);

    // Pelota
    ctx.beginPath();
    ctx.arc(ballX, ballY, 8, 0, Math.PI * 2);
    ctx.fill();
}

function gameLoop() {
    if (!gameRunning) return;

    movePaddles();
    moveBall();
    draw();

    requestAnimationFrame(gameLoop);
}
</script>

</body>
</html>
