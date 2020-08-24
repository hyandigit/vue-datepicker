<template>
  <div id="app">
    <date-picker></date-picker>
  </div>
</template>

<script>

import DatePicker from "./components/datePicker";
import '@/assets/scss/index.scss';
export default {
  name: 'App',
  components: {
    DatePicker

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
</style>
