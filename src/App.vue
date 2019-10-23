<template>
  <div id="app">
    <div class="topLogo">
    <img id="arangologo" alt="ArangoSearch logo" src="./assets/ArangoDBLogo.png">
  </div>
  <div class="imdb-container">
    <h2>Use ArangoSearch to search the <img id="imdblogo" alt="IMDB logo" src="./assets/imdblogo.png"> dataset.</h2>
  </div>
    <Search />
  </div>
</template>

<script>
import Search from './components/Search.vue'

export default {
  name: 'app',
  components: {
    Search
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 1px;
}
#arangologo {
width: 600px;
}
#imdblogo {
  width: 50px;
}
</style>
