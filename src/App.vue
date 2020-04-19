<template>
  <div id="app">
    <ChatBox msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import ChatBox from './components/ChatBox.vue'

export default {
  name: 'App',
  components: {
    ChatBox
  }
}
</script>

<style>
body{
  background: #f9f9f9;
  margin: 0;
  font-size: 1em;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
ul{
  padding: 0;
  margin: 0;
  list-style: none;
}
</style>
