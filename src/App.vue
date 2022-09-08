<template>
  <div id="app">
    <FlightBoard />
  </div>
</template>

<script>
import FlightBoard from './components/FlightBoard.vue'

export default {
  name: 'App',
  components: {
    FlightBoard
  }
}
</script>

<style lang="scss">
#app {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
