<template>
  <div id="app">
    <Board />
  </div>
</template>

<script>
import Board from './views/Board.vue'

export default {
  name: 'App',
  components: {
    Board
  }
}
</script>

<style>
@import './design/style.scss';
</style>
