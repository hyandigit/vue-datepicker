<template>
  <div id="vue-datepicker">
    <date-picker></date-picker>
  </div>
</template>

<script>

import DatePicker from "./components/index";
import '@/assets/scss/index.scss';
export default {
  name: 'vue-datepicker',
  components: {
    DatePicker

  }
}
</script>

<style>
#vue-datepicker {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
