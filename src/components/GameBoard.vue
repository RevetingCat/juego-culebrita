<template>
  <div class="game-board">
    <div
      v-for="(cell, index) in cells"
      :key="index"
      :class="[
        'cell',
        { snake: snakeCells.includes(index), food: food === index }
      ]"
    ></div>
  </div>
</template>

<script>
export default {
  props: {
    cells: Array,
    snakeCells: Array,
    food: Number,
    boardSize: Number,
  },
};
</script>

<style scoped>
.game-board {
  display: grid;
  grid-template-columns: repeat(20, 20px);
  grid-template-rows: repeat(20, 20px);
  gap: 1px;
  border: 2px solid #333;
}

.cell {
  width: 20px;
  height: 20px;
  background-color: #eee;
}

.cell.snake {
  background-color: green;
}

.cell.food {
  background-color: red;
}
</style>
