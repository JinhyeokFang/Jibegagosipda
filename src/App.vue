<template>
  <div id="app">
    <DDay />
  </div>
</template>

<script>
import DDay from './components/d-day.vue'

export default {
  name: 'App',
  components: {
    DDay
  }
}
</script>

<style>
  * {
    font-family: 'Nanum Pen Script', cursive;
  }
  body {
    margin: 0;
  }
  #app {
    display: flex;
    justify-content: center;
    align-items: center;
    min-width: 100vw;
    min-height: 100vh;

    background-color: #4158D0;
    background-image: linear-gradient(43deg, #4158D0 0%, #C850C0 46%, #FFCC70 100%);
  }
</style>
