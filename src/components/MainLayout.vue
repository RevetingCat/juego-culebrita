<template>
    <div>
      <MainHeader />
    </div>
    <div>
      <MainGame />
    </div>
  </template>
  
  <script>
  
  import MainHeader from './MainHeader.vue';
  import MainGame from './MainGame.vue';
  
  export default {
    name: "MainLayout",
    components: {
        MainHeader,
        MainGame
    },
  };
  </script>
  
  <style scoped>
  </style>
  