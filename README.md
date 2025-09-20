# jhm5-ex03

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe Game</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #1a2a6c);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            max-width: 800px;
            width: 100%;
            background-color: rgba(255, 255, 255, 0.92);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            padding: 30px;
            text-align: center;
        }
        
        h1 {
            color: #1a2a6c;
            font-size: 3rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        }
        
        .subtitle {
            color: #b21f1f;
            font-size: 1.2rem;
            margin-bottom: 30px;
        }
        
        .game-info {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            background-color: #f0f0f0;
            padding: 15px;
            border-radius: 10px;
        }
        
        .player-info {
            text-align: left;
            padding: 10px;
        }
        
        .player-info h3 {
            color: #1a2a6c;
            margin-bottom: 5px;
        }
        
        .status {
            font-size: 1.4rem;
            font-weight: bold;
            background-color: #1a2a6c;
            color: white;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
        }
        
        .game-board {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            max-width: 450px;
            margin: 0 auto 30px;
        }
        
        .cell {
            background-color: #fff;
            border: 2px solid #1a2a6c;
            border-radius: 10px;
            aspect-ratio: 1/1;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 3.5rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .cell:hover {
            background-color: #f0f8ff;
            transform: scale(1.03);
        }
        
        .cell.x {
            color: #b21f1f;
        }
        
        .cell.o {
            color: #1a2a6c;
        }
        
        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 20px;
        }
        
        button {
            background: linear-gradient(to right, #1a2a6c, #b21f1f);
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: 1.1rem;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }
        
        button:active {
            transform: translateY(1px);
        }
        
        .mode-selector {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 15px;
        }
        
        .mode-btn {
            background: #f0f0f0;
            color: #1a2a6c;
            border: 2px solid #1a2a6c;
            padding: 10px 20px;
            font-weight: bold;
        }
        
        .mode-btn.active {
            background: linear-gradient(to right, #1a2a6c, #b21f1f);
            color: white;
        }
        
        .winning-cell {
            background-color: rgba(178, 31, 31, 0.2);
            animation: pulse 1.5s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .instructions {
            background-color: #f0f0f0;
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
            text-align: left;
        }
        
        .instructions h3 {
            color: #1a2a6c;
            margin-bottom: 10px;
        }
        
        .instructions ul {
            padding-left: 20px;
        }
        
        .instructions li {
            margin-bottom: 8px;
            line-height: 1.4;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>TIC-TAC-TOE</h1>
        <p class="subtitle">Play against the computer or challenge a friend!!!</p>
        
        <div class="game-info">
            <div class="player-info">
                <h3>Player 1</h3>
                <div>X - Human</div>
            </div>
            <div class="player-info">
                <h3>Player 2</h3>
                <div id="player2-info">O - Human</div>
            </div>
        </div>
        
        <div class="status" id="status">Player X's Turn</div>
        
        <div class="game-board" id="board">
            <div class="cell" data-index="0"></div>
            <div class="cell" data-index="1"></div>
            <div class="cell" data-index="2"></div>
            <div class="cell" data-index="3"></div>
            <div class="cell" data-index="4"></div>
            <div class="cell" data-index="5"></div>
            <div class="cell" data-index="6"></div>
            <div class="cell" data-index="7"></div>
            <div class="cell" data-index="8"></div>
        </div>
        
        <div class="controls">
            <button id="restart-btn">Restart Game</button>
        </div>
        
        <div class="mode-selector">
            <button class="mode-btn" id="two-player-btn">2 Players</button>
            <button class="mode-btn" id="one-player-btn">1 Player</button>
        </div>
        
        <div class="instructions">
            <h3>How to Play:</h3>
            <ul>
                <li>Players take turns placing X and O marks on the 3x3 grid</li>
                <li>The first player to get 3 of their marks in a row (horizontally, vertically, or diagonally) wins</li>
                <li>If all 9 squares are filled and no player has 3 in a row, the game is a draw</li>
                <li>Switch between 1-player (vs computer) and 2-player modes using the buttons above</li>
            </ul>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Game elements
            const board = document.getElementById('board');
            const cells = document.querySelectorAll('.cell');
            const status = document.getElementById('status');
            const restartBtn = document.getElementById('restart-btn');
            const onePlayerBtn = document.getElementById('one-player-btn');
            const twoPlayerBtn = document.getElementById('two-player-btn');
            const player2Info = document.getElementById('player2-info');
            
            // Game state
            let currentPlayer = 'X';
            let gameActive = true;
            let gameMode = 'twoPlayer'; // 'onePlayer' or 'twoPlayer'
            let gameState = ['', '', '', '', '', '', '', '', ''];
            
            // Winning combinations
            const winningConditions = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], // rows
                [0, 3, 6], [1, 4, 7], [2, 5, 8], // columns
                [0, 4, 8], [2, 4, 6]             // diagonals
            ];
            
            //messages
            const winMessage = () => `Player ${currentPlayer} Wins!`;
            const drawMessage = () => `Game Ended in a Draw!`;
            const currentPlayerTurn = () => `Player ${currentPlayer}'s Turn`;
            
            // initialize game
            function initGame() {
                gameActive = true;
                currentPlayer = 'X';
                gameState = ['', '', '', '', '', '', '', '', ''];
                status.textContent = currentPlayerTurn();
                
                //clear board
                cells.forEach(cell => {
                    cell.textContent = '';
                    cell.classList.remove('x', 'o', 'winning-cell');
                });
            }
            
            // handle cell click
            function handleCellClick(clickedCellEvent) {
                const clickedCell = clickedCellEvent.target;
                const clickedCellIndex = parseInt(clickedCell.getAttribute('data-index'));
                
                // Check cell is already played or game is inactive
                if (gameState[clickedCellIndex] !== '' || !gameActive) {
                    return;
                }
                
                // process move
                processMove(clickedCellIndex, clickedCell);
                
                //for 1-player mode, let computer make a move if game is still active
                if (gameMode === 'onePlayer' && gameActive && currentPlayer === 'O') {
                    setTimeout(makeComputerMove, 500);
                }
            }
            
            //process a move
            function processMove(cellIndex, cellElement) {
                // Update game state and UI
                gameState[cellIndex] = currentPlayer;
                cellElement.textContent = currentPlayer;
                cellElement.classList.add(currentPlayer === 'X' ? 'x' : 'o');
                
                //check for win or draw
                if (checkWin()) {
                    status.textContent = winMessage();
                    gameActive = false;
                    highlightWinningCells();
                    return;
                } else if (checkDraw()) {
                    status.textContent = drawMessage();
                    gameActive = false;
                    return;
                }
                
                //switch player
                currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
                status.textContent = currentPlayerTurn();
            }
            
            // check win
            function checkWin() {
                for (let i = 0; i < winningConditions.length; i++) {
                    const [a, b, c] = winningConditions[i];
                    if (gameState[a] !== '' && 
                        gameState[a] === gameState[b] && 
                        gameState[a] === gameState[c]) {
                        return true;
                    }
                }
                return false;
            }
            
            // highlight winning cells
            function highlightWinningCells() {
                for (let i = 0; i < winningConditions.length; i++) {
                    const [a, b, c] = winningConditions[i];
                    if (gameState[a] !== '' && 
                        gameState[a] === gameState[b] && 
                        gameState[a] === gameState[c]) {
                        cells[a].classList.add('winning-cell');
                        cells[b].classList.add('winning-cell');
                        cells[c].classList.add('winning-cell');
                        break;
                    }
                }
            }
            
            // check for draw
            function checkDraw() {
                return !gameState.includes('');
            }
            
            // computer move 
            function makeComputerMove() {
                if (!gameActive) return;
                
                // try to win if possible
                for (let i = 0; i < gameState.length; i++) {
                    if (gameState[i] === '') {
                        gameState[i] = 'O';
                        if (checkWin()) {
                            processMove(i, cells[i]);
                            return;
                        }
                        gameState[i] = '';
                    }
                }
                
                // block player from winning
                for (let i = 0; i < gameState.length; i++) {
                    if (gameState[i] === '') {
                        gameState[i] = 'X';
                        if (checkWin()) {
                            gameState[i] = '';
                            processMove(i, cells[i]);
                            return;
                        }
                        gameState[i] = '';
                    }
                }
                
                // take center
                if (gameState[4] === '') {
                    processMove(4, cells[4]);
                    return;
                }
                
                // take a corner
                const corners = [0, 2, 6, 8];
                const availableCorners = corners.filter(index => gameState[index] === '');
                if (availableCorners.length > 0) {
                    const randomCorner = availableCorners[Math.floor(Math.random() * availableCorners.length)];
                    processMove(randomCorner, cells[randomCorner]);
                    return;
                }
                
                // take any available edge
                const edges = [1, 3, 5, 7];
                const availableEdges = edges.filter(index => gameState[index] === '');
                if (availableEdges.length > 0) {
                    const randomEdge = availableEdges[Math.floor(Math.random() * availableEdges.length)];
                    processMove(randomEdge, cells[randomEdge]);
                    return;
                }
            }
            
            // switch to 1-player mode
            function setOnePlayerMode() {
                gameMode = 'onePlayer';
                onePlayerBtn.classList.add('active');
                twoPlayerBtn.classList.remove('active');
                player2Info.textContent = 'O - Computer';
                initGame();
            }
            
            // switch to 2-player mode
            function setTwoPlayerMode() {
                gameMode = 'twoPlayer';
                twoPlayerBtn.classList.add('active');
                onePlayerBtn.classList.remove('active');
                player2Info.textContent = 'O - Human';
                initGame();
            }
            
            // svent listeners
            cells.forEach(cell => cell.addEventListener('click', handleCellClick));
            restartBtn.addEventListener('click', initGame);
            onePlayerBtn.addEventListener('click', setOnePlayerMode);
            twoPlayerBtn.addEventListener('click', setTwoPlayerMode);
            
            // initialize the game
            setTwoPlayerMode();
        });
    </script>
</body>
</html>
