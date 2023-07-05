<template>
  <div id="app">
    <h2>Tic Tac Toe Widget</h2>
    <div class="board">
      <div v-for="(cell, index) in board" :key="index" class="cell" @click="makeMove(index)">
        {{ cell }}
      </div>
    </div>
    <button @click="resetBoard">Reset</button>
    <p v-if="!gameOver">{{ status }}</p>
    <p v-else>Game Over!</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      board: Array(9).fill(""),
      currentPlayer: "X",
      gameOver: false,
    };
  },
  computed: {
    status() {
      return `Player ${this.currentPlayer}'s turn`;
    },
  },
  methods: {
    makeMove(index) {
      if (!this.board[index] && !this.gameOver) {
        this.board.splice(index, 1, this.currentPlayer);
        this.currentPlayer = this.currentPlayer === "X" ? "O" : "X";
        this.checkWinner();
      }
    },
    checkWinner() {
      const winningCombos = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];

      for (let combo of winningCombos) {
        const [a, b, c] = combo;
        if (this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c]) {
          this.gameOver = true;
          setTimeout(() => {
            alert(`Player ${this.board[a]} wins!`);
          }, 100);
          return;
        }
      }

      if (this.board.every((cell) => cell)) {
        this.gameOver = true;
        setTimeout(() => {
          alert("Draw Game!");
        }, 100);
      }
    },
    resetBoard() {
      this.board = Array(9).fill("");
      this.currentPlayer = "X";
      this.gameOver = false;
    },
  },
};
</script>

<style scoped>
#app {
  text-align: center;
}

h2 {
  font-size: 24px;
  margin-bottom: 20px;
}
.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
  max-width: 300px;
  margin: 0 auto;
  padding: 10px;
  box-sizing: border-box;
}

.cell {
  width: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100px;
  border: 1px solid black;
  cursor: pointer;
  font-size: 24px;
}

.cell:hover {
  background-color: #797979;
}

button {
  margin-top: 10px;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #2196f3;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background-color: #1976d2;
}

button:active {
  background-color: #1565c0;
}

button:focus {
  outline: none;
}

@media (max-width: 480px) {
  .board {
    max-width: 250px;
  }

  .cell {
    width: 70px;
    height: 70px;
    font-size: 18px;
  }

  button {
    font-size: 14px;
  }
}
</style>
