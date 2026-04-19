<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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
    <h1>Pong Game</h1>
    <div id="scoreboard">
        Player 1: <span id="player1Score">0</span> | Player 2: <span id="player2Score">0</span>
    </div>
    <canvas id="gameCanvas" width="800" height="400"></canvas>
    <div id="controls">
        <button id="startButton">Start Game</button>
        <button id="resetButton">Reset Game</button>
        <p>Player 1: Use W (up) and S (down) keys</p>
        <p>Player 2: Use Up Arrow (up) and Down Arrow (down) keys</p>
    </div>
    <script>
        // JavaScript code for the pong game will go here
        let player1Score = 0;
        let player2Score = 0;

        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');

        document.getElementById('startButton').addEventListener('click', startGame);
        document.getElementById('resetButton').addEventListener('click', resetGame);

        function startGame() {
            // Start game logic
        }

        function resetGame() {
            player1Score = 0;
            player2Score = 0;
            updateScoreboard();
        }

        function updateScoreboard() {
            document.getElementById('player1Score').innerText = player1Score;
            document.getElementById('player2Score').innerText = player2Score;
        }
    </script>
</body>
</html>
