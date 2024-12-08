<html>
<head>
<style>
body {
  font-family: sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
  background-color: #333;
  color: #eee;
}

#board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
  gap: 10px; 
}

.cell {
  width: 100px;
  height: 100px;
  background-color: #555;
  border: none;
  font-size: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

#watermark {
  position: fixed;
  bottom: 10px;
  right: 10px;
  font-size: 12px;
  color: rgba(255, 255, 255, 0.5); 
}

</style>
</head>
<body>

<div id="board"></div>

<script>
const board = document.getElementById('board');
let currentPlayer = 'X';
let gameBoard = ['', '', '', '', '', '', '', '', ''];
let gameActive = true;

for (let i = 0; i < 9; i++) {
  const cell = document.createElement('div');
  cell.classList.add('cell');
  cell.id = i;
  cell.addEventListener('click', handleClick);
  board.appendChild(cell);
}

function handleClick(e) {
  const cellIndex = parseInt(e.target.id);

  if (gameBoard[cellIndex] === '' && gameActive) {
    gameBoard[cellIndex] = currentPlayer;
    e.target.textContent = currentPlayer;
    if (checkWin()) {
      alert(`Player ${currentPlayer} wins!`);
      gameActive = false;
    } else if (checkDraw()) {
      alert("It's a draw!");
      gameActive = false;
    } else {
      currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    }
  }
}

function checkWin() {
  const winPatterns = [
    [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
    [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
    [0, 4, 8], [2, 4, 6]            // Diagonals
  ];

  for (const pattern of winPatterns) {
    const [a, b, c] = pattern;
    if (gameBoard[a] && gameBoard[a] === gameBoard[b] && gameBoard[a] === gameBoard[c]) {
      return true;
    }
  }

  return false;
}

function checkDraw() {
    return gameBoard.every(cell => cell !== '');
}

</script>

<div id="watermark">Made with love by @aawaramalik007</div>

</body>
</html>
