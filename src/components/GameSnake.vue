<template>

  <div class="MainDiv">
    <div @keydown="handleKey" tabindex="0">
    <div>    <GameBoard
      :cells="cells"
      :snakeCells="snake"
      :food="food"
      :boardSize="boardSize"
    /></div>
  </div>
  </div>

</template>

<script>
import GameBoard from "./GameBoard.vue";

export default {
  components: { GameBoard },
  props: {
    boardSize: {
      type: Number,
      default: 20,
    },
  },
  data() {
    return {
      cells: Array(400).fill(null),
      snake: [44, 43, 42],
      direction: "RIGHT",
      food: null,
      score: 0,
    };
  },
  mounted() {
    this.spawnFood();
    this.startGame();
  },
  methods: {
    startGame() {
      window.addEventListener("keydown", this.handleKey);
      this.gameInterval = setInterval(this.moveSnake, 200);
    },
    handleKey(event) {
      switch (event.key) {
        case "ArrowUp":
          if (this.direction !== "DOWN") this.direction = "UP";
          break;
        case "ArrowDown":
          if (this.direction !== "UP") this.direction = "DOWN";
          break;
        case "ArrowLeft":
          if (this.direction !== "RIGHT") this.direction = "LEFT";
          break;
        case "ArrowRight":
          if (this.direction !== "LEFT") this.direction = "RIGHT";
          break;
      }
    },
    moveSnake() {
      const head = this.snake[0];
      let newHead;

      switch (this.direction) {
        case "UP":
          newHead = head - this.boardSize;
          break;
        case "DOWN":
          newHead = head + this.boardSize;
          break;
        case "LEFT":
          newHead = head - 1;
          break;
        case "RIGHT":
          newHead = head + 1;
          break;
      }

      if (
        newHead < 0 ||
        newHead >= this.cells.length ||
        (this.direction === "LEFT" && newHead % this.boardSize === this.boardSize - 1) ||
        (this.direction === "RIGHT" && newHead % this.boardSize === 0) ||
        this.snake.includes(newHead)
      ) {
        alert("Moriste! Puntuación: " + this.score);
        clearInterval(this.gameInterval);
        this.resetGame();
        return;
      }

      if (newHead === this.food) {
        this.snake.unshift(newHead);
        this.score += 1;
        this.$emit("updateScore", this.score);
        this.spawnFood();
      } else {
        this.snake.unshift(newHead);
        this.snake.pop();
      }
    },
    spawnFood() {
      let newFood;
      do {
        newFood = Math.floor(Math.random() * this.cells.length);
      } while (this.snake.includes(newFood));
      this.food = newFood;
    },
    resetGame() {
      this.snake = [44, 43, 42];
      this.direction = "RIGHT";
      this.food = null;
      this.score = 0;
      this.$emit("updateScore", this.score);
      this.spawnFood();
      this.startGame();
    },
  },
  beforeUnmount() {
    clearInterval(this.gameInterval);
    window.removeEventListener("keydown", this.handleKey);
  },
};
</script>

<style scoped>
.MainDiv {
  display: flex;
  justify-content: center;
  align-items: center;
  height: auto;
}

</style>