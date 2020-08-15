<template>
  <div id="app">
    <Board />
  </div>
</template>

<script>
import Board from './views/MainBoard.vue'

export default {
  name: 'App',
  components: {
    Board
  }
}
</script>

<style>
@import './design/style.css';
</style>
