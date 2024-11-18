<template>
    <div class="MainDiv">
      <GameSnake gridSize="10" :cellSize="50">
        <GameBoard></GameBoard>
      </GameSnake>
    </div>
  </template>
  
  <script>
  import GameBoard from './GameBoard.vue';
  import GameSnake from './GameSnake.vue';
  
  export default {
    name: 'MainGame',
    components: {
      GameBoard,
      GameSnake,
    },
  };
  </script>
  
  <style>
  </style>
  