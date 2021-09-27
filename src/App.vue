<template>
  <div id="app">
    <hand/>
  </div>
</template>

<script>
import hand from '@/components/Hand.vue'

export default {
  name: 'App',
  components: {
    hand
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
