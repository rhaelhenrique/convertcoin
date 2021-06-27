<template>
  <div id="app">
    <Convert />
  </div>
</template>

<script>
import Convert from './components/Convert.vue';

export default {
  name: 'App',
  components: {
    Convert
  }
}
</script>

<style>
  html, body {
    margin: 0;
    padding: 0;
    background-color: #f2f2f2;
  }
</style>
