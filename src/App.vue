<template>
  <MainLayout/>
</template>

<script>
import MainLayout from './components/MainLayout.vue'

export default {
  name: 'App',
  components: {
    MainLayout
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #2e2e2e;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

</style>
