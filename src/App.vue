<template>
  <div id="app">
    <c-calc/>
    <notifications position="bottom left"/>
  </div>
</template>

<script>
import cCalc from './components/c-calc.vue'

export default {
  name: 'App',
  components: {
    cCalc
  }
}
</script>

<style>
@import "./style/reset.css";

@font-face {
  font-family: 'pock';
  src: url("./assets/fonts/pock.TTF") format("truetype");
  font-weight: normal;
  font-style: normal;
}

#app {
  font-family: ds-digitalnormal, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #f9e8ef;

  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  align-items: center;

  min-height: 100vh;
  width: 100%;
  height: 100%;
}
</style>
